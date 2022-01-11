<template>
    <div class="container">
      <h4 class="text-end m-3">Pozdravljeni, <b>Admin</b>!</h4>
      <div class="row justify-content-center align-items-center text-start">
        <div class="col-md-6">
          <h2>Vloge:</h2>
          <div class="accordion" id="accordionExample">
              <Vloga v-for="(item, i) in parsedVloge" :key="item" :id="i" :vloga="item"/>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vloga from '../components/Vloga.vue';
export default {    
    components: {
        Vloga
    },
    data() {
      return {
        parsedVloge: [],
        isAccepted: false
      };
    },
    mounted() {
      let tempVloge = localStorage.getItem("vloge")
      this.parsedVloge = JSON.parse(tempVloge);
    }
}
</script>