<template>
  <div>
    <form @submit.prevent="onSubmit">
      <div class="form-group">
        <input type="text" v-model="product.name" class="form-control">
      </div>
      <div class="form-group">
        <input type="text" v-model="product.price" class="form-control">
      </div>
      <input type="file" @change="onFileSelected">
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>

  <router-link to="/">Back</router-link>
  </div>
    
</template>

<script>
import axios from 'axios'
export default {
  props: ['id'],
  
  data(){
    return{
      product: [],
      selectedFile: null
    }
  },

  methods: {
    async fethcProduct(){
      const {data} = await axios.get(`/products/${this.id}`)
      this.product = data
    },

    async onSubmit(){
      const formData = new FormData();
      formData.append('product[photo]', this.selectedFile)
      await axios.put(`/products/${this.id}`, formData)
      this.$router.push('/')
    },

    onFileSelected(event){
      this.selectedFile = event.target.files[0]
    }
  },

  beforeMount(){
    this.fethcProduct()
  }

}
</script>

