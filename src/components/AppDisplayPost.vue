<template>
  <div class="productCard">
    <div class="image">
      <a>
        <img :src="product.images[0].src">
      </a>
    </div>
    <div class="cost">
      {{ product.variants[0].price }}$
    </div>
    <a class="title">
      <span v-html="product.title" />
    </a>
  </div>
</template>

<script>
export default {
  props: {
    product: {
    	required: true,
    	default: null
   	},
    searchTerm: {
      required: false,
      default: null
    }
  },
  methods: {
    // add span tags with the hl-search CSS class to the search term.
    highlightData( data ) {
      if ( this.searchTerm ) {
        const pattern = new RegExp( this.searchTerm, 'i' );
        const highlightedData = data.replace(
          pattern,
          `<span class="hl-search">${this.searchTerm}</span>`
        );
        return highlightedData;
      }
    }
  }
};
</script>

<style lang="scss">
  .productCard {
    display: flex;
    flex-direction: column;
    max-width: 20%;
    padding: 5px;
    margin-left: 15px;
    margin-right: 15px;
    margin-bottom: 20px;
    box-shadow: 0 0 0 1px #ececec;

    img {
      width: 200px;
      height: 150px;
    }

    .title {
      margin-top: 10px;
      font-size: 18px;

    }

    .cost {
      margin-top: 10px;
      font-size: 18px;
      font-weight: bold;
      text-align: center;
    }
  }

</style>
