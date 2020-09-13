<template>
  <div class="card mb-4 shadow">
    <div class="card-img-top">
      <img :src="item.item_photo" class="w-100 h-100">
    </div>
    <div class="card-body">
      <h4 class="card-title text-success">{{item.item_name}}</h4>
      <p class="card-text ">{{ item.item_desc }} is a good taste and healthy food for you.</p>
      <router-link :to="{name: 'item-show', params: { id: item.item_id }}" class="btn btn-success   mr-2">Detail</router-link>
      <button @click="addToCart()" class="btn btn-outline-success">Add to Cart</button>
    </div>
  </div>
</template>

<script type="text/javascript">
  export default{
    props:{
      item: Object
    },
    methods: {
      addToCart() {
        let myitem = {id:this.item.item_id,name:this.item.item_name,price:this.item.item_price,qty:1};
        this.$store.dispatch('addToCart', myitem)
      }
    }
  };
</script>

<style type="text/css">
  .card{
    transition: .5s;
  }
  .card:hover{
    transform: translateY(-20px);
  }
  .card-img-top{
    overflow: hidden;
  }
  .card img{
    transition: .5s;
  }
  .card:hover img{
    transform: scale(1.1);
  }
</style>