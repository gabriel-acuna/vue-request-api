<template>
  <div class="column is-12-mobile is-4-desktop is-4-tablet">
    <div class="card">
      <div class="card-header">
        <img :src="character.image" :alt="character.name" />
      </div>
      <div class="card-content">
        <h3 class="title is-size-4">Name: {{character.name}}</h3>
        <button class="button is-success is-rounded" @click="showModal(character.id)">View more</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CharacterCard",
  props: {
    character: Object
  },
  methods:{
      showModal(id){
          this.$emit('showModal', id);
      }
  }
};
</script>
