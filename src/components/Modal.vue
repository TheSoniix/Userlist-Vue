<template>
  <div>
    <b-modal id="bv-modal-edit">
      <modal-header>
        <template></template>
      </modal-header>

      <template #default="{}">
        <form>
          <div class="form-group">
            <div>
              <label>Id</label>
              <b-form-input disabled type="text" class="form-control" id="id" v-model="userId"></b-form-input>
              <label>Firstname</label>
              <b-form-input type="text" class="form-control" id="firstname" v-model="userFirstname"></b-form-input>
              <label>Secondname</label>
              <b-form-input type="text" class="form-control" id="firstname" v-model="userSecondname"></b-form-input>
              <label>Description</label>
              <b-form-textarea type="text" class="form-control" id="firstname" v-model="userDescription"></b-form-textarea>
            </div>
          </div>
        </form>
      </template>

      <template #modal-footer="{submit, close}">
        <b-button variant="primary" type="button"
                  v-on:click="$emit('edit-user', [Number(userId), userFirstname, userSecondname, userDescription])">
          Save
        </b-button>
        <b-button variant="dark" @click="close()">Close</b-button>
      </template>
    </b-modal>
  </div>

</template>

<script>
import Vue from 'vue';

export default Vue.extend({
  name: "Modal",
  props: {
    id: String,
    firstname: String,
    secondname: String,
    description: String
  },
  data: function () {
    return {
      userId: '',
      userFirstname: '',
      userSecondname: '',
      userDescription: ''

    }
  },
  watch: {
    id: function (newVal) {
      this.userId = newVal;
    },
    firstname: function (newVal) {
      this.userFirstname = newVal;
    },
    secondname: function (newVal) {
      this.userSecondname = newVal;
    },
    description: function (newVal) {
      this.userDescription = newVal;
    }
  }
});
</script>

<style scoped>
</style>
