<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      characters: [],
      filterCharacter: '',
      page: 1,
      info: {},
    };
  },

  methods: {
    fetch(url) {
      const newUrl = url.split('&name=')[0];
      let result = axios
        .get(`${newUrl}&name=${this.filterCharacter}`)
        .then((res) => {
          this.characters = res.data.results;
          this.info = res.data.info;
          this.page = newUrl.split('page=')[1];
        })
        .catch((err) => {
          console.log(err);
        });
    },
    Clean() {
      let result = [];
      this.characters = result;
      this.filterCharacter = '';
    },
    handleSearch() {
      this.fetch('https://rickandmortyapi.com/api/character/?page=1');
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
      />
      <span class="icon is-left">
        <i class="fas fa-search" aria-hidden="true"></i>
      </span>
    </p>
    <br />
    <button class="button is-success" v-on:click="handleSearch">
      Consultar
    </button>
    <button
      v-if="characters.length > 0"
      class="button is-danger"
      v-on:click="Clean"
    >
      Limpiar
    </button>
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
  </div>
  <nav
    class="is-flex is-justify-content-center my-2"
    role="navegation"
    aria-label="pagination"
    v-if="characters.length > 0"
  >
    <button :disabled="!info.prev" class="button" v-on:click="fetch(info.prev)">
      Anterior
    </button>
    <button class="button is-primary mx-2">{{ page }}</button>
    <button :disabled="!info.next" class="button" v-on:click="fetch(info.next)">
      Siguiente
    </button>
  </nav>

  <footer class="footer">
    <div class="content has-text-centered">
      <p>
        <strong>Project Api Vue Js</strong> by
        <spam class="is-size-4 has-text-primary">JP👨‍💻</spam>.
      </p>
    </div>
  </footer>
</template>
