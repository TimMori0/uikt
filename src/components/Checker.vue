<template>
    <div>
        <h4 class="text-end m-3">Pozdravljeni, <b>Uporabnik</b>!</h4>
        <h1 class="p-3">Seznam vlog</h1>
        <div v-for="item in vloge" :key="item">
            {{ item.name }} <div v-if="item.isAccepted == true"><span class="badge bg-success">Accepted</span></div><div v-else-if="item.isAccepted == false"><span class="badge bg-danger">Rejected</span><br/>
            
            Še enkrat preglejte naslednje podatke:
            {{item.name}}, {{item.surname}}, {{ item.birth }}, {{ item.country }}, {{ item.gender }}, {{ item.postal }}, {{ item.place }}

            </div><span class="fw-bold badge bg-secondary" v-else>Neaktivno</span>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            vloge: []
        };
    },
    mounted() {
    let tempVloge = localStorage.getItem("vloge")
    let parsedVloge = JSON.parse(tempVloge);
    this.vloge = parsedVloge;
  }
}
</script>