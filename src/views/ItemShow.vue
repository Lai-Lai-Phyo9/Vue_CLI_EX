<template>
  <div class="container">
    <div class="row my-3">
      <div class="col-md-12">
        <h2 class="my-5 text-success">Item Detail</h2>
      </div>
    </div>
    <div class="row p-0">
      <div class="col-md-6 col-12 m-0  border-success p-0 rounded-3">
        <img :src="item.item_photo" style="width:80%;" class="m-0 rounded-3">
      </div>
      <div class="col-md-6 col-12 m-0">
        <table class="table mt-5 text-left table-borderless">
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
        <p>
          <span class="mr-2" v-if="item.brand"> 
            <b-icon icon="tag-fill" variant="success"></b-icon> {{item.brand.brand_name}}
          </span>
<!--           <span v-if="item.subcategory">
            <b-icon icon="tag-fill" variant="dark"></b-icon> {{item.subcategory.subcategory_name}}
          </span> -->
        </p>
        <div class="text-left">
          <input type="number" name="qty" v-model="qty" class="form-control w-25 d-inline-block" min="1">
          <button class="ml-3 btn btn-outline-success" @click="addToCart()">Add To Cart</button>
        </div>
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