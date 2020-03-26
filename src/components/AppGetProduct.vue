<template>
  <div class="products">
      <!-- AppDisplayPost Component -->
      <app-display-post v-for="product in productData" :key="product.id" :product="product">
      </app-display-post>
 </div>
</template>


<script>
import axios from 'axios';
import AppDisplayPost from './AppDisplayPost';

export default {
  components: { 'app-display-post': AppDisplayPost },
  data() {
    return {
      apiResponse: '',
      productData: []
    };
  },
  mounted() { this.getPosts(); },
  methods: {
    async getPosts() {
      try {
        const response = await axios("/products.json");
        this.productData = response.data.products;
        this.isDataAvailable = true;
        console.log(response);
        console.log(this.productData);
        // fetch("/products.json")
        //  .then(response => response.json())
        //  .then(({ products }) => {
        //    this.productData = products;
        //    console.log(products);
        //    for (var prop in products) {
        //      console.log("obj." + prop + " = " + products[prop].title);
        //    }
        //  });
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
</style>
