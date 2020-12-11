<!--suppress TypeScriptUnresolvedVariable -->
<template>
  <div>
    <!-- Liste -->
    <b-table-simple hover caption-top>
      <b-thead head-variant="dark">
        <b-tr>
          <b-th>Id</b-th>
          <b-th>Firstname</b-th>
          <b-th>Secondname</b-th>
          <b-th>Description</b-th>
          <b-th>Date</b-th>
          <b-th></b-th>
        </b-tr>
      </b-thead>
      <b-tbody v-for="(user, index) in userlist" v-bind:key="user.id">
        <b-tr>
          <b-th>{{ user.id }}</b-th>
          <b-td>{{ user.firstname }}</b-td>
          <b-td>{{ user.secondname }}</b-td>
          <b-td>{{ user.description }}</b-td>
          <b-td>{{ user.creationTime }}</b-td>
          <b-td>
            <b-button class="btn btn-dark m-1" v-on:click="$emit('openModal', user)">
              Edit
            </b-button>
            <b-button class="btn btn-danger m-1" v-on:click="$emit('delete', index)">
              Delete
            </b-button>
          </b-td>
        </b-tr>
      </b-tbody>
    </b-table-simple>
  </div>

</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "Userlist",
  props: {
    userlist: Array
  }
});
</script>

<style scoped>
</style>
