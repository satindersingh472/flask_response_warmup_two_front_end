<template>
  <div>
    <div class="all_inputs">
      <div class="one_input">
        <p>Name</p>
        <input type="text" ref="name" />
      </div>
      <div class="one_input">
        <p>Description</p>
        <input type="text" ref="description" />
      </div>
      <div class="one_inpu">
        <p>Image_url</p>
        <input type="text" ref="image_url" />
      </div>
    </div>
    <button @click="add_pokemon">Add Pokemon</button>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  methods: {
    add_pokemon() {
      axios
        .request({
          url: `${process.env.VUE_APP_BASE_DOMAIN}/api/pokemon`,
          method: 'POST',
          data: {
            name: this.$refs['name']['value'],
            description: this.$refs['description']['value'],
            image_url: this.$refs['image_url']['value']
          },
        })
        .then((response) => {
          response;
        })
        .catch((error) => {
          error;
        })
    },

    
  },
}
</script>

<style lang="scss" scoped>
.all_inputs{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

</style>
