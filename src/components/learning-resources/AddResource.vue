<template>
  <base-dialog v-if="inputIsInvalid" @close="confirmError">
    <!-- title="Invalid Input" -->
    <template v-slot:default>
      <p>Infelizmente, pelo menos um dos dados está inválido.</p>
      <p>Por favor verifique se não deixou nenhuma informação em branco.</p>
    </template>
    <template v-slot:actions>
      <base-button @click="confirmError">Ok</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Objetivo</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Descrição</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          ref="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link (opcional)</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Adicionar</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
export default {
  components: { BaseButton },
  inject: ['addResource'],

  data() {
    return {
      inputIsInvalid: false,
    };
  },

  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredLink = this.$refs.linkInput.value;
      if (enteredTitle.trim() === '' || enteredDescription.trim() === '') {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(enteredTitle, enteredDescription, enteredLink);
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  },
};
</script>

<style scoped>
input,
textarea {
  border-radius: 10px;
}

label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
