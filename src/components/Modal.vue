<template>
  <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">

      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Create a new ⚡FlashCard</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>

      <div class="modal-body">
        <form @submit.prevent="createCard" action="">
            <div class="form-group">
                <label for="question">Question</label>
                <textarea v-model="currentQuestion" placeholder="Escribe la pregunta" class="form-control" id="question" name="question" rows="3"></textarea>
            </div>
            <div class="form-group">
                <label for="answer">Answer</label>
                <textarea v-model="currentAnswer" placeholder="Escribe la respuesta" class="form-control" id="answer" name="answer" rows="3"></textarea>
            </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button @click="createCard" type="button" class="btn btn-primary" data-bs-dismiss="modal">Save changes</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {  
    name:'Modal',
    props:['cQuestion','cAnswer'],
    emits:['response'],
    data(){
      return{
        cQuest: this.cQuestion,
        cAns: this.cAnswer,
      }
    },    
    methods:{
      createCard(){        
        // Emitimos el evento al padre.
        this.$emit('response', [this.currentQuestion, this.currentAnswer]);
        this.currentQuestion = '';
        this.currentAnswer = '';
      }
    }
}
</script>

<style>

</style>