<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
        <div class="hero-body has-text-centered">
            <p class="title mb-6">
                Welcome to YUR CAR
            </p>
            <p class="subtitle">
                best CAR with good Price
            </p>
        </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
          <h2 class="is-size-2 has-text-centered">Latest Offers</h2>
      </div>

      <div 
        class="column is-3"
        v-for="product in latestProducts"
        v-bind:key="product.id"
        v-bind:product="product" 
      >

        <div class="box">
          <figure class="image mb-4">
            <img :src="product.get_thumbnail">
          </figure>
          <h3 class ="is-size-4">{{product.name}}</h3>
          <p class="is-size-6 has text_grey">MAD{{product.price}}</p>
          View Details
        </div> 
      </div> 
    </div>
  </div>
</template>>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  data() {
    return {
      latestProducts: []
    }
  },
  components: {
  },
  mounted() {
    this.getLatestProducts()
  },
  methods: {
    getLatestProducts() {
      axios
        .get('/api/v1/latest-products/')
        .then(response => {
          this.latestProducts=response.data
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>

<style scooped>
  .image{
    margin-top: -1.25rem;
    margin-left: -1.25rem;
    margin-right: -1.25rem;
  }
</style>