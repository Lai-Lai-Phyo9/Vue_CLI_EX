<template>
	<div class="card shadow mb-4">
		<div class="card-header py-3">
		  <h4 class="m-0 font-weight-bold text-success">order List</h4>
		</div>
		<div class="card-body">
		  <div class="table-responsive">
		    <table class="table table-bordered text-center" id="dataTable" width="100%" cellspacing="0">
		      <thead>
		        <tr>
		        	<th>No</th>
		          <th>Voucher No</th>
		          <th>User Name</th>
		          <th>Total</th>
		          <th>Detail</th>
		        </tr>
		      </thead>
		      <tbody>
	          <tr v-for="currency in info" :key="currency.order_id">
	          	<td>{{qty++}}</td>
	            <td>{{currency.order_voucherno}}</td>
	            <td>{{currency.order_user.user_name}}</td>
	            <td>{{currency.order_total}}</td>
	            <td>
	            	<a href="#" class="badge badge-success">Success</a>
	          	</td>
	          </tr>
        </tbody>
		    </table>
		  </div>
		</div>
	</div>
</template>
<script type="text/javascript">	
import axios from 'axios'
  export default{
    data (){
      return{
      	qty: 1,
        info: Object

      }
    },
    mounted(){
      axios.get('http://osapi.thetpainghtut.com/api/v1/orders')
           .then(res=>{
            this.info=res.data.orders;
           })
    }
  };
</script>
<style type="text/css">
	
</style>