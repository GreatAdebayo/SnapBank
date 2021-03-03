<template>
    <div>
    <div class="container-fluid"> 
    <div class="row mt-3">      
    <div class="col-8 mx-auto pt-3 pb-5 rounded mb-5" id="section" :class="{trans:load}"> 
    <form class="needs-validation w-100" novalidation>

    <small class="font-weight-bold">  <i class="far fa-credit-card text-primary"></i> DEBIT CARD APPLICATION PAGE</small>


    <div class="text-left mt-3" v-for="(item,index) in getmyJSON" :key="index" v-show="userName == item.lastname">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Name on Card</small></label>
    <input :value="item.firstname + ' ' + item.lastname" type="text" class="form-control" id="validationCustom01" disabled>
    </div>

  


    <div class="text-left mt-3">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Card Type</small></label>
    <select  name="gender"  class="form-control">
      <option disabled value="">Please select the card type</option>
      <option>Master Card</option>
      <option>Visa Card</option>
    </select>

    </div> 

     <div class="text-left mt-3">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Shipping Address</small></label>
    <input  name="amount" type="text" class="form-control" id="validationCustom01" placeholder="Address you want your card to be shipped to">
    </div> <br>
    
   <button @click.prevent="deposit" class="btn btn-success px-3"> <small class="font-weight-bold"> APPLY </small></button> 
   
    </form>

     </div>

  
     </div>
 
    </div>

    
    </div>
</template>
<script>
export default {
    name:'Apply',
    data(){
      return{
        userName: this.$route.params.id,
        getmyJSON:''
      }
    },


       created(){
      this.getmyJSON =JSON.parse(localStorage.myUsers)
    }
    
    
}
</script>
<style scoped>
 
</style>