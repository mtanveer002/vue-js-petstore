<template>
    <div class="pat">
      
        <Card  style="width: 25em">
            <template #header>
                <img :src="pat.img" alt="pat" style="height: 15rem" />
            </template>
            <template #title>
               {{ pat.name }}
            </template>
            <template #subtitle>
               Age: {{ pat.age }}
            </template>
            <template #footer>
                <Button 
                    icon="pi pi-times" class="p-button-rounded p-button-danger" 
                    style="margin-right: 4em" 
                    @click="onRemove(pat.id)" 
                />
                <Button 
                    icon="pi pi-heart" :class="[pat.isFavorite ? '' : 'p-button-outlined', 'p-button-rounded','p-button-danger']" 
                    @click="addFav(pat.id)" 
                />
            </template>
        </Card>
    </div>
    
</template>

<script>
export default {
    
    props:{
        pat: Object
    },
    data() {
        return {
           
        };
    },

    mounted() {
        
    },

    methods: {
        onRemove(id){
            // console.log('clicked', id)
            this.$emit("remove-pat", id)
        },
        addFav(id){
            this.$emit("add-fav", id)
        }
    },
};
</script>

<style lang="scss" scoped>

</style>