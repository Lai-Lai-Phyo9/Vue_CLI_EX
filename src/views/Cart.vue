<template>
  <div class="container">
    <section v-if="orderDone" class="my-3">
      <h2 class="text-success">Order Completed Successfully!</h2>
    </section>
    <div class="row">
      <div class="col-12 col-md-7"  id="voucher_div">
        <div class="container p-3 shadow">
          <h3 class="text-center mb-3">Payment</h3>
          <table class="table table-bordered">
              <thead class="thead-light">
                <tr>
                  <th scope="col">No</th>
                  <th scope="col">Name</th>
                  <th scope="col">Price</th>
                  <th scope="col">Qty</th>
                  <th scope="col">Total</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item,index) in cart" :key="index">
                  <td>{{++index}}</td>
                  <td>{{item.name}}</td>
                  <td>{{item.price}}</td>
                  <td>
                      <button class="btn btn-sm btn-outline-danger" @click="addQty(item.id)">+</button> 
                      <input type="text" name="" :value="item.qty" min="1" class="text-center w-25 mx-2 border border-0">             
                      <button class="btn btn-sm btn-outline-danger"  @click="minusQty(item.id)">-</button>
                      <button @click="removeFromCart(item.id)" class="btn btn-sm btn-danger mx-2">Remove</button>
                  </td> 
                  <td>{{item.price*item.qty}} MMK</td>
                </tr>
              </tbody>
          </table>          
        </div>
      </div>
      <div class="col-12 col-md-5">
        <div class="container p-3 shadow">
          <table class="table">
            <tr>
              <th class="text-left">1 Items</th>
              <td class="text-right">10000<span>MMK</span></td>
            </tr>
            <tr>
              <th class="text-left">Shipping</th>
              <td class="text-right"><select>
                      <optgroup>
                        <option>Please select an option</option>
                        <option>1</option>
                        <option>2</option>
                        <option>3</option>
                      </optgroup>
                  </select>
              </td>
            </tr>
            <tr>
              <th class="text-left">Subtotal</th>
              <td class="text-right">4000<span>----MMK</span></td>
            </tr>
            <tr>
              <th class="text-left">Total</th>
              <td class="text-right">10000<span>---MMK</span></td>
            </tr>
          </table>
          <button class="btn btn-success">Check Out</button>
        </div> 
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
  export default{
    computed:{
      cart(){
        return this.$store.state.cart;
      },
    },
    methods:{
      removeFromCart(itemId){
        this.$store.dispatch('removeFromCart',itemId)
      },
      addQty(itemId){
        this.$store.dispatch('addQty',itemId)
      },
      minusQty(itemId){
        this.$store.dispatch('minusQty',itemId)
      }
    }
  };
</script>
