<template>
  <div>
    <add-pokemon></add-pokemon>
    <div v-for="result in results" :key="result['id']">
        <p>id:{{result[0]}}</p>
        <h2>Name: {{result[1]}}</h2>
        <p>Description: {{result[2]}}</p>
        <img :src="result[3]" :alt="`image of ${result[1]}`">
    </div>
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
          url: 'http://127.0.0.1:5000/api/pokemon'
        })
        .then((response) => {
          this.results = response['data']
        })
        .catch((error) => {
          error
        })
    },
  },
  data() {
    return {
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
    width: 100%;
    height: 300px;
    object-fit: cover;
}

</style>
