<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      characters: [],
    };
  },

  methods: {
    fetch() {
      let result = axios
        .get('https://rickandmortyapi.com/api/character')
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
  },
};
</script>

<template>
  <div>
    <h1 class="title">Consumir Api</h1>
    <button class="button is-success" v-on:click="fetch">Consultar</button>
    <button class="button is-danger" v-on:click="Clean">Limpiar</button>
  </div>

  <div class="container">
    <div
      class="columns is-desktop is-mobile is-tablet is-multiline is-centered"
    >
      <div
        class="column is-12-mobile is-4-desktop is-4-tablet"
        v-for="character of characters"
        v-bind:key="character.id"
      >
        <div class="card">
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
