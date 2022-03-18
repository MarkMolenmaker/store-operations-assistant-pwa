<template>
  <div class='wrapper'>
    <form @submit.prevent='search' class='search-bar'>
      <input type='text' placeholder='Zoek een artikel' name='search-product' v-model='search_query' autocomplete='off'>
      <a @click='search'><i class='icon orange fas fa-search'/></a>
    </form>
    <div class='search-product-results'>
      <SearchProductLine @add-product="add_product" class="search-item" v-for="element in search_results" v-bind:key="element.sku" :img="element.images[0].effectiveUrl" :title="element.name" :sku="element.sku"/>
    </div>
    <a v-if="search_results.length > 1" @click="clear_results" class="clear-results red noselect">Resultaten wissen</a>
  </div>
</template>

<script>
import SearchProductLine from '@/components/SearchProductLine'
export default {
  name: 'SearchProductInput',
  components: { SearchProductLine },
  emits: ['addOrderLine'],
  data () {
    return {
      search_query: '',
      search_results: []
    }
  },
  methods: {
    search () {
      fetch(`https://api.coop.nl/INTERSHOP/rest/WFS/COOP-3645-Site/-;loc=nl_NL;cur=EUR/culios/products?searchTerm=${this.search_query}&amount=9`, {
        method: 'GET',
        credentials: 'omit',
        headers: {
          Accept: 'application/json',
          'Accept-Language': 'nl,en-US;q=0.7,en;q=0.3',
          'content-type': 'application/json',
          'Sec-Fetch-Dest': 'empty',
          'Sec-Fetch-Mode': 'cors',
          'Sec-Fetch-Site': 'same-site'
        },
        referrer: 'https://www.coop.nl/',
        mode: 'cors'
      }).then(response => response.json())
        .then(json => {
          this.search_results = json.elements
        })
    },
    add_product (title, sku, img) {
      this.$emit('addOrderLine', title, sku, img)
    },
    clear_results () {
      this.search_results = []
      this.search_query = ''
    }
  }
}
</script>

<style scoped>
  .search-bar {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    margin-bottom: .5em;
  }
  input {
    color: var(--black-color);
    padding: .5em;
    width: 100%;
  }
  .clear-results { text-decoration: underline; }
  .search-item { }
  .icon { font-size: 1.5em; margin-left: .7em; }
</style>
