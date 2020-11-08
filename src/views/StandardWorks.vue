<template>
<div class="page">
  <Search :title="'Standard Works'" :filters="pageFilters" @filters-updated="updateActiveFilters"/>
  <div class="graph-container">
    <BarGraph :chart-data="datacollection"></BarGraph>
  </div>
  <div class="instruction-container">
    <h3>Information</h3>
    <p>The Standard Works word analysis graph lets you compare the frequency and use of single words across the entire
      standard works library including the Old Testament, the New Testament, The Book of Mormon, the Doctrine and
      Covenants and The Pearl of Great Price. Search for any word using the filters to filter by work to see data represented in a bar graph.
      Any number of words can be searched at once to see comparisons between words. Multiple words should be entered as a comma seperated list.</p>
  </div>
</div>
</template>

<script>
import Search from "../components/Search.vue"
import BarGraph from '../components/BarGraph.vue'
export default {
  name: 'StandardWorks',
  components: {
    Search,
    BarGraph
  },
  data() {
    return {
      datacollection: null,
      activeFilters: [],  //TODO right a function to add/remove filters from this list when they are checked or unchecked
      pageFilters: [
        this.$root.$data.books.ot,
        this.$root.$data.books.nt,
        this.$root.$data.books.bom,
        this.$root.$data.books.dc,
        this.$root.$data.books.pogp,
      ],
    }
  },
  mounted() {
    this.fillData()
  },
  methods: {
    fillData() {
      this.datacollection = {
        labels: [],
        datasets: []
      };
      let wordData = this.$root.$data.wordData;
      for(let word of wordData) {
        this.datacollection.labels.push(word.word);
      }
      for(let filter of this.activeFilters) {
        let dataSet = {
          label: filter.label,
          backgroundColor: filter.color,
          data: []
        };
        for(let word of wordData){
          dataSet.data.push(word.instances[filter.short]);
        }
        this.datacollection.datasets.push(dataSet);
      }
    },
    updateActiveFilters(newActiveFilters) {
      this.activeFilters = newActiveFilters;
      this.fillData();
    }
  }
}
</script>

<style scoped>
.graph-container {
  max-width: 900px;
  margin: 20px auto;
}
</style>
