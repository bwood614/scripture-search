<template>
<div class="wrapper">
  <form id="searchForm" class="search-form">
    <div class="page-title">
      {{title}}
    </div>
    <div class="search-container">
      <input class="search-button" type="image" src="/images/search-icon.png" border="0" alt="Submit" />
      <input id="searchBar" class="form-control" type="text" placeholder="Search any word" aria-label="Search">
    </div>
    <div class="filter-container">
      <div class="filter-item" v-for="filter in filters" :key="filter.filterId">
        <label v-if="filter.filterType === 'checkbox'" :for="filter.filterId">
          <input type="checkbox" :id="filter.filterId" :name="filter.label" :value="filter" v-model="activeFilters">
          {{filter.label}}
        </label>
        <input v-else-if="filter.filterType === 'date'" :id="filter.filterId" type="text" :placeholder="filter.short" :aria-label="filter.filterId">
      </div>
    </div>
  </form>
</div>
</template>

<script>
export default {
  name: 'Search',
  props: {
    title: String,
    filters: Array,
  },
  data() {
    return {
      activeFilters: []
    }
  },
  watch: {
    // whenever question changes, this function will run
    activeFilters: function () {
      this.$emit('filters-updated', this.activeFilters);
    }
  },
  methods: {
  }
}
</script>

<style scoped>
.search-form {
  width: 80%;
  margin: 0px auto;
  margin-top: 30px;
}

.search-container {
  display: flex;
  align-items: center;
}

.search-button {
  width: 30px;
  height: 30px;
  margin-right: 4px;
}

.page-title {
  font-size: 35px;
  font-weight:500;
  margin-bottom: 15px;
}

.filter-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 15px;
}

/* Mobile Styles */
@media only screen and (max-width: 500px) {
  .search-form {
    width: 90%;
  }

  .filter-container {
    flex-direction: column;
  }
}

/* Desktop Styles */
@media only screen and (min-width: 501px) {
  .filter-container {
    justify-content: space-around;
  }
}
</style>
