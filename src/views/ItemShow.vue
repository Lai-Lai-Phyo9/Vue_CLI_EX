<template>
  <div class="container my-4">
    <h1 class="text-success my-4">Item Detail</h1>   
  <div class="row">
    <div class="col-md-6 col-12">
      <img :src="item.item_photo" class="w-50 h-100">
    </div>
    <div class="col-md-6 col-12">
      <table class="table">
        <tr>
          <td>Name</td>
          <td>{{item.item_name}}</td>
        </tr>
        <tr>
          <td>Code</td>
          <td>{{item.item_code}}</td>
        </tr>
        <tr>
          <td>Price</td>
          <td>{{item.item_price}}</td>
        </tr>
        <tr>
          <td>Discount</td>
          <td>{{item.item_discount}}%</td>
        </tr>
      </table>
      <div class="text mb-5">
          <span class="text-success">BRAND:</span>{{item.brand.brand_name}}.{{item.subcategory.subcategory_name}}
          <p class="text-success">Description:<span class="text-secondary">{{item.item_desc}}</span></p>
      </div>
      <input type="number" name="qty" v-model="qty" class="form-control w-25 d-inline-block" min="1">

      <button class="ml-3 btn btn-info" @click="addToCart()">Add To Cart</button>
    </div>
  </div>
</div>
</template>


<script type="text/javascript">
  import ItemService from '@/services/ItemService.js'

  export default{
    data(){
      return{
        qty: 1,
        item : {}
      }
    },
    created(){
      let id = this.$route.params.id;
      ItemService.getItem(id)
        .then(response => {
          this.item = response.data.item
        })
        .catch(error => {
          console.log('There was an error:',error.response)
        })
    },
    methods: {
      addToCart() {
        let item = {id:this.item.item_id,name:this.item.item_name,price:this.item.item_price,qty:this.qty};
        this.$store.dispatch('addToCart', item)
      }
    }
  };
</script>

<style type="text/css">
  
</style>
