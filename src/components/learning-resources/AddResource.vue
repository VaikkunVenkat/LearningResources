<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <template #default>
      <p>Unfortunately one input value is invalid</p>
      <p>check inputs - make sure to add characters to each field</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="title" v-model="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          type="text"
          name="description"
          id="description"
          v-model="description"
        />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" name="link" id="link" v-model="link" />
      </div>
      <base-button type="submit"> Add Resource </base-button>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      description: '',
      link: '',
      inputIsInvalid: false,
    };
  },
  inject: ['addResource'],
  methods: {
    submitData() {
      if (
        this.title.trim() === '' ||
        this.description.trim() === '' ||
        this.link === ''
      ) {
        this.inputIsInvalid = true;
      } else {
        this.addResource(this.title, this.description, this.link);
      }
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  },
};
</script>

<style scoped>
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
