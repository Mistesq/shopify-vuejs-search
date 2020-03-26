<template>
  <div>
    <!-- Search Box -->
    <div class="search">
      <input
        v-model.lazy="searchTerm"
        type="text"
        class="form-control"
        placeholder="Search titles"
        aria-label="Search" >
      <div class="input-group-append">
        <span>Search</span>
      </div>
    </div> <!-- .input-search -->

    <!-- AppGetPosts Component -->
    <app-get-product
      :search-term="searchTerm"
    />

  </div>
</template>

<script>
import AppGetProduct from './AppGetProduct';

export default {
	components: {
		'app-get-product': AppGetProduct
	},
	data() {
		return {
			searchTerm: ''
		};
	}
};
</script>

<style lang="scss">
  .search {
    text-align: center;

    input {
      padding: 10px;
      font-size: 22px;
    }

    .input-group-append {
      margin-top: 10px;
      font-size: 22px;
    }
  }
</style>
