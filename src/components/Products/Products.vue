<template>
  <div>
    <table class="table">
      <thead>
        <th>Name</th>
        <th>Description</th>
        <th>Price</th>
        <th>Picture</th>
        <th></th>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{product.name}}</td>
          <td>{{product.description}}</td>
          <td>{{product.price}}</td>
          <td>
            <img :src="product.file_url" alt="" height="150" width="110">
          </td>
          <td>
            <div class="btn-group" role="group" aria-label="Basic example">
              <!-- <router-link :to="{ name: 'editBook', params: { id: book.id }}">{{book.name}}</router-link> -->
              <router-link :to="{name: 'editProduct', params: {id: product.id}}">
                <button type="button" class="btn btn-secondary">Edit</button>
              </router-link>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data(){
    return {
        products: []
    }
  },

  methods: {
    async fetchProducts(){
        const {data} = await axios.get(`/products`)
        this.products = data
    }
  },

  beforeMount(){
    this.fetchProducts()
  }
}
</script>

