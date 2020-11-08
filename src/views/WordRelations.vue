<template>
<div class="page">
  <Search :title="'Chronological Analysis'" :filters="pageFilters" @filters-updated="updateActiveFilters" />
  <div class="instruction-container">
    <h3>Information</h3>
    <p>Word Relations is a way to visualize links and connections between different words in the scriptures.
    When a word is searched, every verse that contains that word will be searched for other common words. a
    list of these connected words is then returned in order of frequency.</p>
  </div>
</div>
</template>

<script>
import Search from "../components/Search.vue"
export default {
  name: 'WordRelations',
  components: {
    Search
  },
  data() {
    return {
      activeFilters: [],
      pageFilters: [
        this.$root.$data.books.ot,
        this.$root.$data.books.nt,
        this.$root.$data.books.bom,
        this.$root.$data.books.dc,
        this.$root.$data.books.pogp,
      ],
    }
  },
  methods: {
    updateActiveFilters(newActiveFilters) {
      this.currentFilter = newActiveFilters[0];
      this.fillData();
    }
  }
}
</script>

<style scoped>
</style>
