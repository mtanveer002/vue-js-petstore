<template>
  <div class="home">
    <Addpat @add-pat="addPat"/>
    <Pats @remove-pat="removePat" @add-fav="addFav" :pats="pats" />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Pats from '../components/Pats.vue';
import Addpat from '../components/Addpat.vue';

@Options({
  components: {
  Pats,
  Addpat,
  },
  methods: {
    // addPat(pat){
    //   this.pats = [...this.pats, pat];
    // }
    async addPat(pat) {
      const res = fetch('https://637e90ec5b1cc8d6f9307861.mockapi.io/pats',{
        method: "POST",
        headers: {
          "content-type": "application/json",
        },
        body: JSON.stringify(pat),
      })

      const data = await res.json();
      this.pats = [...this.pats, data];
    },
    async removePat(id){
      if(confirm("Are you sure to remove pet from list")){
        // this.pats = this.pats.filter((pat) => pat.id !== id)
        const res = await fetch(`https://637e90ec5b1cc8d6f9307861.mockapi.io/pats/${id}`,{
          method: "DELETE",
        });
        res.status === 200 ? (this.pats = this.pats.filter((pat) => pat.id !== id)) : "Faild to Delete"
      }
    },
    async addFav(id){
      // this.pats = this.pats.map((pat) => pat.id === id ? {...pat, isFavefort: !pat.isFavefort} : pat)
      const addFavorite = await this.fetchPat(id);
    
      const updatedFavorite = {...addFavorite.isFavorite, isFavorite: !addFavorite.isFavorite}
      const res = await fetch(`https://637e90ec5b1cc8d6f9307861.mockapi.io/pats/${id}`, {
        method: "PUT",
        headers: { "content-type": "application/json" },
        body: JSON.stringify(updatedFavorite)
      })
      this.pats = this.pats.map((pat) => pat.id === id ? {...pat, isFavefort: !pat.isFavefort} : pat);
      const data = await res.json();  
      this.pats = this.pats.map((pat) => pat.id === id ? {...pat, isFavorite: data.isFavorite} : pat);
    },

   async fetchPats(){
    const res = await fetch('https://637e90ec5b1cc8d6f9307861.mockapi.io/pats');
    const data = await res.json();
   
    
    return data;
   },
   async fetchPat(id){
    const res = await fetch(`https://637e90ec5b1cc8d6f9307861.mockapi.io/pats/${id}`);
    const data = await res.json();
    return data;
   }
  },
  data(){
    return{
         pats:[]
    }
  },
  async created() {
        this.pats = await this.fetchPats();
        
        
      // this.pats = [
      //       {
      //         id: 1,
      //         name: "Ruby",
      //         age: 2,
      //         img: 'https://www.primefaces.org/wp-content/uploads/2020/02/primefacesorg-primevue-2020.png',
      //         isFavefort: true
      //       },
      //       {
      //         id: 2,
      //         name: "Coco",
      //         age: 4,
      //         img: 'https://www.primefaces.org/wp-content/uploads/2020/02/primefacesorg-primevue-2020.png',
      //         isFavefort: false
      //       },
      //       {
      //         id: 3,
      //         name: "Tomy",
      //         age: 6,
      //         img: 'https://www.primefaces.org/wp-content/uploads/2020/02/primefacesorg-primevue-2020.png',
      //         isFavefort: false
      //       }
      // ]
  },
})
export default class HomeView extends Vue {
[x: string]: unknown;
}
</script>
