<template>
  <div>
    <div v-for="product in productData" :key="product.id">
        <a href="{{ product.url | within: collection }}">{{ product.title }}</a>
        {{ product.price | money }}
        <a href="{{ product.url | within: collection }}">
          <img src="{{ product.featured_image.src | img_url: 'large' }}" alt="{{ product.featured_image.alt | escape }}">
        </a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      productData: []
    };
  },
  mounted() {
    fetch("/products.json")
     .then(response => response.json())
     .then(({ products }) => {
       this.productData = products;
       console.log(products);
       for (var prop in products) {
         console.log("obj." + prop + " = " + products[prop].title);
       }
     });
  }
};

</script>
