<template>
    <form @submit="onSubmit" class="p-fluid grid m-4">
        <div class="field col-12 md:col-2">
            <span class="p-float-label">
                <InputText id="name" v-model="name" type="text" />
                <label for="name">name</label>
            </span>
        </div>
        <div class="field col-12 md:col-2">
            <span class="p-float-label">
                <InputText id="age" v-model="age" type="number"  />
                <label for="age">age</label>
            </span>
        </div>
        <div class="field col-12 md:col-2">
            <span class="p-float-label">
                <InputText id="img" v-model="url" type="text"  />
                <label for="img">Image URL</label>
            </span>
        </div>
        <div class="field col-12 md:col-2">
            <Button icon="pi pi-plus" type="submit" label="Add" class="p-button p-button-success" style="margin-right: 4em"/>
        </div>
    </form>
    
</template>

<script>
export default {
    name: 'PetstoreVueAddpat',

    data() {
        return {
           name: "",
           age: "",
           img: ""
        };
    },

    mounted() {
        
    },

    methods: {
        onSubmit(e){
            e.preventDefault();

            const newPat = {
                name : this.name,
                age : this.age,
                img : this.url,
                isFavorite : false
            }

            this.$emit("add-pat", newPat);
            this.name = '';
            this.age = '';
            this.url = '';
        }

        
    },
};
</script>

<style lang="scss" scoped>

</style>