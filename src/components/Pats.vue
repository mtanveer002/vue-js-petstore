<template>
    <div class="flex gap-4 p-grid">
        <div class="p-col-12 p-md-6 p-lg-3" v-for="pat in pats" :key="pat.id">
           
            <Pat @remove-pat="$emit('remove-pat', pat.id)" @add-fav="$emit('add-fav', pat.id)" :pat="pat" />

        </div>
    </div>
</template>

<script>
    import Pat from './Pat.vue';

    export default {
        name: 'PetstoreVuePets',
        props:{ pats: Array },
        components: { Pat },
        emits: ["remove-pat", "add-fav"],
        
        data() {
            return {
            
            };
        },

        mounted() {
            
        },

        methods: {
            
        },
    };
</script>

<style lang="scss" scoped>

</style>