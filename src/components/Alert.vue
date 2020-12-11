<template>
  <div>
    <b-alert show="" variant="success">
      <div class="d-flex justify-content-center">
       <div>
         {{ message }}
       </div>
     </div>
    </b-alert>
  </div>

</template>

<script>
import Vue from 'vue';

export default Vue.extend({
  name: "Alert",
  props: {
    message: String,
  }
})
</script>

<style scoped>

</style>
