<template>
 
    <div class="modal-card">
      <header class="modal-card-head">
          <p class="modal-card-title"> {{character.name}}</p>
      </header>
      <section class="modal-card-body">
        <p>Gender: {{character.gender}}</p>
        <p>Status: {{character.status}}</p>
        <p>Species: {{character.species}}</p>
        <p>Type: {{character.type}}</p>
      </section>
      <!-- <footer class="modal-card-footer">
            <button class="button">x</button>
      </footer> -->
    </div>
</template>

<script>
export default {
  name: "DetailModal",
  props: {
    character: Object
  }
};
</script>

