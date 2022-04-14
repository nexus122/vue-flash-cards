<template>
  <main>
    <div class="container">
      <!-- Titulo y btn de agregar -->
      <h1>FlashCards</h1>
      <button
        @click="clearTarget"
        type="button"
        data-bs-toggle="modal"
        data-bs-target="#exampleModal"
        class="btn btn-primary"
      >
        <i class="fa-solid fa-plus"></i> Add Card
      </button>
      <hr />
      <!-- Contenedor de las tarjetas -->
      <div class="row row-cols-1 row-cols-md-2 g-4">
        <div
          class="note--panel col"
          v-for="nota in notas.sort((a, b) =>
            a.id < b.id ? -1 : b.id > a.id ? 1 : 0
          )"
          :key="nota.id"
        >
          <Card
            @editCard="
              (paramID) => {
                // Buscamos el elemento con la id de parmID
                let temp = this.notas.find((nota) => nota.id == paramID);
                this.currentQuestion = temp.question;
                this.currentAnswer = temp.answer;
                this.currentId = temp.id;
              }
            "
            @deleteCard="
              (paramId) =>
                (this.notas = this.notas.filter((nota) => nota.id != paramId))
            "
            :card="nota"
          ></Card>
        </div>
      </div>

      <!-- Modal -->
      <!-- Esto deberia ser otro componente, pero no me da la vida -->
      <div
        class="modal fade"
        id="exampleModal"
        tabindex="-1"
        aria-labelledby="exampleModalLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">
                Create a new ⚡FlashCard
              </h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>

            <div class="modal-body">
              <form @submit.prevent="createCard" action="">
                <div class="form-group">
                  <label for="question">Question</label>
                  <textarea
                    v-model="currentQuestion"
                    placeholder="Escribe la pregunta"
                    class="form-control"
                    id="question"
                    name="question"
                    rows="3"
                  ></textarea>
                </div>
                <div class="form-group">
                  <label for="answer">Answer</label>
                  <textarea
                    v-model="currentAnswer"
                    placeholder="Escribe la respuesta"
                    class="form-control"
                    id="answer"
                    name="answer"
                    rows="3"
                  ></textarea>
                </div>
              </form>
            </div>
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary"
                data-bs-dismiss="modal"
              >
                Close
              </button>
              <button
                @click="createCard"
                type="button"
                class="btn btn-primary"
                data-bs-dismiss="modal"
              >
                Save changes
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import Card from "./components/Card.vue";
export default {
  data() {
    return {
      // Contenido de los inputs
      currentQuestion: "",
      currentAnswer: "",
      currentId: 0,
      // Grupo de notas.
      notas: [
        {
          id: 1,
          question: "Tu primera nota",
          answer: "Si, de verdad, es la primera !",
        },
        {
          id: 2,
          question: "Tu segunda nota",
          answer: "Si, de verdad es la segunda!",
        },
      ],
    };
  },
  components: {
    Card,
  },
  methods: {
    createCard() {
      let tempId = this.currentId;

      if (tempId != 0) {
        this.notas = this.notas.filter((nota) => nota.id != tempId);
      } else {
        tempId = Date.now();
      }

      // Creamos una nueva tarjeta
      this.notas.push({
        id: tempId,
        question: this.currentQuestion,
        answer: this.currentAnswer,
      });
      this.clearTarget();
    },
    clearTarget() {
      this.currentQuestion = "";
      this.currentAnswer = "";
      this.currentId = 0;
    },
  }
};
</script>

<style>
</style>