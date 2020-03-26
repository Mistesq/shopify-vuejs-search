<template>
  <div v-if="isDataAvailable">

    <!-- Number of Products -->
    <p class="count" v-if="filteredResults.length === productData.length">
      {{ productData.length }} Posts
    </p>
    <p class="count" v-else>
      Found {{ filteredResults.length }} of {{ productData.length }}
    </p>

    <div class="products">

      <app-display-post
       v-for="product in filteredResults"
        :key="product.id"
        :search-term="searchTerm"
        :product="product"
         role="article">
      </app-display-post>

    </div>

  </div>

  <div v-else>
    <p
      class="text-center"
      v-html="apiResponse" />
  </div>
</template>


<script>
import axios from 'axios';
import AppDisplayPost from './AppDisplayPost';

export default {
  components: { 'app-display-post': AppDisplayPost },
  props: {
		searchTerm: {
			type: String,
			default: ''
		}
  },
  data() {
    return {
      apiResponse: '',
      productData: [],
      isDataAvailable: false
    };
  },
  computed: {
    filteredResults() {
      if ( this.productData ) {
        const pattern = new RegExp( this.searchTerm, 'i' ); // match keyword against post titles or excerpts.
        const filteredProducts = this.productData.filter( prod => {
          return (
            prod.title.match(pattern)
          );
        });
        return filteredProducts;
        console.log(filteredProducts);
        console.log(pattern);
      }
    },
  },
  mounted() { this.getPosts(); },
  methods: {
    async getPosts() {
      try {
        const limit = 20;
        const response = await axios(`/products.json?&limit=${limit}`);
        this.productData = response.data.products;
        this.isDataAvailable = true;
        console.log(response);
        console.log(this.productData);

        }
        catch ( error ) {
        	this.apiResponse = ` The request could not be processed! <br> <strong>${error}</strong> `;
        }
      }
  }
};

</script>

<style lang="scss">
  .products {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }

  .count {
    font-size: 25px;
  }
</style>
