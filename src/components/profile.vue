<template>
    <div>
      <div class="container-fluid">
        <div class="row color">
        <div class="col-md mt-5 text-left mx-auto mb-5">
        <i class="fas fa-user-circle text-primary fa-3x ml-2"></i>
        <p class="font-weight-bold text-left ml-2">Basic Data</p>

        
       <form class="w-100" v-for="(item,index) in getmyJSON" :key="index" v-show="userName == item.customerId">
       <div class="form-group">
       <p class="font-weight-bold text-left ml-2">Account Number: {{item.acnumber}}</p>
   
       <label for="exampleInputEmail1"><small class="font-weight-bold"> Firstname</small></label>
       <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="item.firstname" disabled>
       </div>

       <div class="form-group">
       <label for="exampleInputEmail1"><small class="font-weight-bold"> Last name</small></label>
       <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="item.lastname"  disabled>
       </div>

        <div class="form-group">
       <label for="exampleInputEmail1"><small class="font-weight-bold"> Middle name</small></label>
       <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="item.middlename"  disabled>
       </div>


      <div class="form-group">
      <label for="exampleInputEmail1"><small class="font-weight-bold"> Phone Number</small></label>
      <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="item.mobile"  disabled>
      </div>

      <div class="form-group">
      <label for="exampleInputEmail1"><small class="font-weight-bold"> Email address</small></label>
      <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="item.email" disabled>
      </div>
  
      </form>
      <div class="alert alert-primary mt-3" role="alert">
      <small class="font-weight-bold"><i class="fas fa-info-circle"></i> You can not change any of your informations here. To change your account information please send an email to contact@snapbank.com </small>
      </div>       

      </div>

      

          </div>
          
    </div> 
    </div>
</template>
<script>
export default {
    name: 'Profile',
    data(){
        return{
       getmyJSON:'',
        userName: this.$route.params.id,
        }
    },


     created(){
      this.getmyJSON =JSON.parse(localStorage.myUsers)
    }
  
}
</script>
<style>
    
</style>