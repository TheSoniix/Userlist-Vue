<template>
  <div>
    <h5>New User</h5>
    <form v-on:submit.prevent="$emit('add-user', [firstname, secondname, description]); clear()">
      <div class="form-group">
        <label for="firstNameInput">Firstname</label>
        <input type="text" class="form-control" id="firstNameInput" v-model="firstname">
        <label for="secondNameInput">Secondname</label>
        <input type="text" class="form-control" id="secondNameInput" v-model="secondname">
        <span>Description</span>
        <b-form-textarea type="text" class="form-control" id="descriptionInput" v-model="description"></b-form-textarea>
      </div>
      <button type="submit" class="btn btn-success">Add</button>
    </form>
  </div>
</template>

<script>
import Vue from 'vue';


export default Vue.extend({
  name: "AddFormular",
  data() {
    return {
      firstname: '',
      secondname: '',
      description: '',
    }
  },
  methods: {
    clear: function () {
      this.firstname = '';
      this.secondname = '';
      this.description = '';
    }
  }
});
</script>

<style scoped>
</style>
