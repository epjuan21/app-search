<template>
  <div class="hello">
    <input type="text" name="" id="" v-model="query"/>
    <button v-on:click="getQuery">Buscar</button>
    <p>{{ query }}</p>

    <small>{{ items }}</small>

  </div>
</template>

<script>

export default {
  name: "SearchItems",

  data() {
    return {
      items: [],
      query: ''
    };
  },

  methods: {
    fetchItems(url) {
      fetch(url)
        .then(stream => stream.json())
        .then(data => (this.items = data));
    },

    getQuery () {
      let url = `https://www.datos.gov.co/resource/i7cb-raxc.json?$where=producto like'%25${this.query}%25'`
      this.fetchItems(url)      
    }

  },  
};
</script>

<style scoped>

</style>