<template>
    <div>
        <h1 class="text-success p-5">Vloga oddana v predogled!</h1>
        <button v-if="isAdmin" class="btn btn-danger" @click="Preview()">Preglej vlogo!</button>
    </div>
</template>

<script>
export default {
    methods: {
        Preview() {
            this.$router.push( { name: 'Preview' } )
        }
    },
    props: {
        isAdmin: Boolean
    }
}
</script>