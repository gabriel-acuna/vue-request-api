<template>
  <div id="app">
    <div class="hero is-white is-gradient is-bold">
      <div class="hero-body">
        <h1 class="title">
          <span class="has-text-success">Rick & Morty</span>
          <span class="subtitle">Characters</span>
        </h1>
        <div class="field has-addons is-pulled-right">
          <div class="control">
            <input type="text" class="input is-rounded" v-model="search" @keyup.enter="searchCharacter">
          </div>
         <div class="control">
            <button  class="button is-success is-rounded" @click="searchCharacter">Search</button>
         </div>

        </div>
      </div>
    </div>

    <div class="container">
      <div class="columns is-desktop is-mobile is-tablet is-multiline is-centered">
        
        <CharacterCard @showModal="showModal" :character="character" v-for="character in characters" :key="character.id" />
      </div>
      <nav class="pagination is-centered" role="navigation" aria-label="pagination">
        <a class="pagination-previous" @click="changePage(page-1)">Previous</a>
        <a class="pagination-next" @click="changePage(page+1)">Next page</a>
        <ul class="pagination-list">
          <li>
            <a class="pagination-link is-current">{{page}}</a>
          </li>
        </ul>
        
      </nav>
    </div>

    <div class="modal" :class="{'is-active': modal}">
      <div class="modal-background" @click="modal=false"></div>
      <DetailModal :character="currentCharacter" />
      <button class="modal-close is-large" aria-label="close" @click="modal=false"></button>
    </div>
  </div>
</template>

<script>
import CharacterCard from "./components/CharacterCard";
import DetailModal from "./components/DetailModal";

export default {
  name: "App",
  components: { 
    CharacterCard,
    DetailModal
    },
  data: function() {
    return {
      characters: [],
      currentCharacter: {},
      page: 1,
      pages: 1,
      search: '',
      modal: false
    };
  },
  created() {
    this.getData();
  },
  methods: {
    async getData() {
      try {
        let url = new URL("https://rickandmortyapi.com/api/character");
        url.search = new URLSearchParams({ page: this.page, name: this.search });
        let response = await fetch(url);
        let { info, results } = await response.json();
        this.characters = results;
        this.pages = info.pages;
      } catch (error) {
        throw new Error(error);
      }
    },
    changePage (page) {
      this.page = page <= 0 || page > this.pages ? this.page : page;
      this.getData();
    },
    searchCharacter (){
      this.page=1;
      this.getData();
    },
    showModal(id){
      this.getCharacter(id);

    },
    async getCharacter(id){
      let response = await fetch(`https://rickandmortyapi.com/api/character/${id}`);
      this.currentCharacter = await response.json();
      this.modal = true;  

    }

  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
