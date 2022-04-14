<template>
  <div class="card">
    <!-- Cuerpo de la tarjeta -->
    <div class="card-body">
      <h5 class="card-title">{{ card.question }}</h5>
      <a @click="showAnswer = !showAnswer" class="card-link">Show Answer</a>
      <p v-show="showAnswer" class="card-text">
        {{ card.answer }}
      </p>

      <!-- Botones -->
      <div class="btnOptions">
        <button @click="editCard(card.id)" data-bs-toggle="modal" data-bs-target="#exampleModal" class="btn btn-success">Edit</button>
        <button @click="deleteCard(card.id)" class="btn btn-danger">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["card"],
  data() {
    return {
      showAnswer: false,
    };
  },
  emits:['deleteCard', 'editCard'],
  methods:{
      deleteCard(param){
          // Emitimos un evento al padre para que borre la nota, con el id de la card.          
          this.$emit('deleteCard', param);
      },
      editCard(param){
        // Emitimos un evento al padre para que borre la nota, con el id de la card.        
        this.$emit('editCard', param);
      }
  }
};
</script>

<style scoped>
a {
  cursor: pointer;
}
.btnOptions {
  display: flex;
  justify-content: space-between;  
}
</style>