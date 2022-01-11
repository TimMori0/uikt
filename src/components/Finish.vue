<template>
    <div>
        <h1 class="text-success p-5">Proces je bil uspešno dokončan!</h1>
    </div>
</template>

<script>
export default {
    methods: {
        Preview() {
            this.$router.push( { name: 'Preview' } )
        }
    }
}
</script>