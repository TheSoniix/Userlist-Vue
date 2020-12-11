<template>
  <div id="app">

    <!-- Navbar -->
    <b-navbar type="dark" variant="dark">
      <b-navbar-brand>
        {{ message }}
      </b-navbar-brand>
    </b-navbar>

    <!-- Alert -->
    <div v-for="(alert, index) in alerts" v-bind:key="index" class="d-flex justify-content-center mt-3">
      <Alert class="w-25" v-bind:message="alert"></Alert>
    </div>

    <!-- Add -->
    <div class="d-flex justify-content-center mt-3">
      <AddFormular class="w-25" v-on:add-user="add($event)"></AddFormular>
    </div>

    <!-- Userlist -->
    <div class="d-flex justify-content-center mt-3">
      <Userlist class="w-50"
                v-bind:userlist="userlist"
                v-on:delete="deleteUser($event)"
                v-on:openModal="openModal($event)">
      </Userlist>
    </div>

    <!-- Modal -->
    <Modal
        :id="id"
        :firstname="firstname"
        :secondname="secondname"
        :description="description"
        v-on:edit-user="save($event)">
    </Modal>

  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Userlist from './components/Userlist.vue';
import AddFormular from './components/AddFormular.vue';
import {User} from "@/Model/User";
import Modal from './components/Modal.vue';
import {ModalPlugin} from 'bootstrap-vue'
import Alert from "@/components/Alert.vue";

Vue.use(ModalPlugin)

export default Vue.extend({
  name: 'App',
  components: {
    Userlist,
    AddFormular,
    Modal,
    Alert
  },
  data() {
    return {
      message: 'Userlist-Vue',
      id: '',
      firstname: '',
      secondname: '',
      description: '',
      alerts: [''],
      userlist: [
        new User('Julian', 'Scheffler', 'Der aller coolste'),
        new User('Angelina', 'Schartner', 'Die aller schönste')
      ],
    }
  },
  created() {
    this.alerts.splice(0,1)
  },
  methods: {
    add: function (content: string[]) {
      if (content[0].trim().length > 0 && content[1].trim().length > 0 && content[2].trim().length > 0) {
        const newUser = new User(content[0], content[1], content[2])
        this.$data.userlist.push(newUser);
        this.alerts.push(newUser.firstname);
        setTimeout(() => {this.alerts.splice(0, 1);},5000);
      } else console.log('Wrong Input!')
    },
    deleteUser: function (index: number) {
      this.alerts.push(this.userlist[index].firstname);
      this.$data.userlist.splice(index, 1);
      setTimeout(() => {this.alerts.splice(0, 1);},5000)
    },
    save: function (editUser: [number, string, string, string]) {
      this.$bvModal.hide('bv-modal-edit');
      this.userlist.forEach((user: User) => {
        if (user.id == editUser[0]) {
          this.alerts.push(user.firstname);
          setTimeout(() => {this.alerts.splice( 0, 1);},5000)
          user.firstname = editUser[1];
          user.secondname = editUser[2];
          user.description = editUser[3];
        }
      });
    },
    openModal: function (user: User) {
      this.id = String(user.id);
      this.firstname = user.firstname;
      this.secondname = user.secondname;
      this.description = user.description;
      this.$bvModal.show('bv-modal-edit');
    }
  }
});
</script>

<style>

</style>
