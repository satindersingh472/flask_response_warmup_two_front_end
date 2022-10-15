<template>
  <div>
    <add-pokemon></add-pokemon>
    <div v-for="result in results" :key="result['id']">
        <p>id:{{result[0]}}</p>
        <h2>Name: {{result[1]}}</h2>
        <p>Description: {{result[2]}}</p>
        <img :src="result[3]" :alt="`image of ${result[1]}`">
    </div>
    <h2 v-if="message != undefined" >
      {{message}}
    </h2>
  </div>
</template>

<script>
import axios from 'axios';
import AddPokemon from '@/components/addPokemon.vue';
export default {
    components: {
        AddPokemon,
    },
    mounted () {
        this.all_pokemons();
    },
  methods: {
    all_pokemons() {
      axios
        .request({
          url: `${process.env.VUE_APP_BASE_DOMAIN}/api/pokemon`
        })
        .then((response) => {
          if(response['data'] === "No results for your inout"){
            this.message = response['data']
          } else{
            this.results = response['data']
          }
        })
        .catch((error) => {
          this.message = error;
        })
    },
  },
  data() {
    return {
        message: undefined,
        results: undefined
    }
  },
}
</script>

<style lang="scss" scoped>
*{
    padding: 0px;
    margin: 0px;
}
img{
    width: 300px;
    height: 300px;
    object-fit: cover;
}

</style>
