<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      characters: [],
      filterCharacter: '',
    };
  },

  methods: {
    fetch() {
      const params = {
        name: this.filterCharacter,
      };
      let result = axios
        .get('https://rickandmortyapi.com/api/character/', { params })
        .then((res) => {
          this.characters = res.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    Clean() {
      let result = [];
      this.characters = result;
    },
    handleSearch() {
      this.fetch();
    },
  },
};
</script>

<template>
  <nav class="panel is-primary">
    <h1 class="panel-heading panel-title">Rick and Morty API</h1>
  </nav>

  <div class="search-button">
    <p class="control has-icons-left">
      <input
        v-model="filterCharacter"
        class="input is-primary"
        type="text"
        placeholder="Search"
        v-on:keyup.enter="handleSearch"
        v-if="characters.length > 0"
      />
      <span class="icon is-left">
        <i class="fas fa-search" aria-hidden="true"></i>
      </span>
    </p>
    <br />
    <button class="button is-success" v-on:click="handleSearch">
      Consultar
    </button>
    <button class="button is-danger" v-on:click="Clean">Limpiar</button>
  </div>
  <br />
  <div class="container">
    <div
      class="columns is-desktop is-mobile is-tablet is-multiline is-centered"
    >
      <div
        class="column is-12-mobile is-4-desktop is-4-tablet"
        v-for="character of characters"
        v-bind:key="character.id"
      >
        <div class="card card-style">
          <div class="card-image justify-content-center">
            <figure class="image is-128x128">
              <img :src="character.image" class="" />
            </figure>
          </div>
          <div class="card-content">
            <div class="media">
              <div class="media-left">
                <h1 class="title is-size-5">Name:</h1>
              </div>
              <h1>{{ character.name }}</h1>
            </div>
            <div class="media">
              <div class="media-left">
                <h1 class="title is-size-5">Type:</h1>
              </div>
              <p v-if="character.type == ''">Not type</p>
              <p v-else>{{ character.type }}</p>
            </div>
            <div class="media">
              <div class="media-left">
                <p class="title is-size-5">Status:</p>
              </div>
              <p>{{ character.status }}</p>
            </div>
          </div>
          <footer class="card-footer">
            <spam class="tag is-success mt-2">{{ character.status }}</spam>
          </footer>
        </div>
      </div>
    </div>

    <!-- <div class="card-image">
      <img src="{{character.image}}" alt="" />
    </div>
    <div class="card-content">
      <h1>{{ character.name }}</h1>
    </div> -->
  </div>
</template>
