<template>
    <div>
         <!-- NAV BAR STARTS -->
    <nav class="navbar navbar-expand-md bg-primary navbar-light fixed-top">
       <router-link to="/" class="navbar-brand"> <h5 class="text-left font-weight-bold text-light ml-3">
    <i class="fas fa-poo-storm"></i> SnapBank</h5>
    </router-link>
    <button class="navbar-toggler custom-toggler" type="button" data-toggle="collapse" 
    data-target="#collapsibleNavbar" aria-controls="collapsibleNavbar" aria-expanded="false" 
    aria-label="Toggle navigation">
    <span class=" navbar-toggler-icon "></span>
    </button>
    <div class="collapse navbar-collapse" id="collapsibleNavbar">

    <ul class="navbar-nav ml-auto mr-2 px-5 text-center">
    <li class="nav-item pt-2">
    <a class="nav-link text-light font-weight-bold"><strong><i class="fas fa-lock"></i> Log In</strong></a>
    </li>
    </ul>


    </div>  
    </nav>
    
   <!-- NAV BAR ENDS -->   
     <!-- LOG IN FORM STARTS    -->
    <div class="container-fluid"> 
    <div class="row mt-5">      
    <div class="col-6 mx-auto p-5 mt-5 rounded" id="section"> 
    <h5 class="text-center font-weight-bold text-primary ml-3">
    <i class="fas fa-poo-storm"></i> SnapBank</h5>
      
    <form class="w-100 needs-validation" >
     <small class="font-weight-bold ml-3"><i class="fas fa-user-circle text-primary"></i> ONLINE BANKING PAGE</small>
    <div class="form-row">
    <div class="col-md-6 mt-5 text-left text-primary">
    <label for="validationCustom01"><small class="font-weight-bold"><i class="fas fa-user"></i>  Email </small></label>
    <input  v-model="email" name="email" type="email" class="form-control" id="validationCustom08" placeholder="email">
    </div>

    <div class="col-md-6  mt-5 text-left text-primary">
    <label for="validationCustom02"><small class="font-weight-bold"><i class="fas fa-unlock"></i> Password</small></label>
    <input v-model="password" name="password" type="password" class="form-control" id="validationCustom09" placeholder="password">
   
     </div>
     </div>
     
     <button  @click.prevent="loginPage" class="btn btn-primary btn-sm  mt-3 mb-2 px-4"> <small class="font-weight-bold"> LOGIN </small> <i class="fas fa-sign-out-alt"></i></button> <br>
   
     <small class="ml-3 font-weight-bold color">Forgot password? <span class="text-primary"> <i @click="resetPassword" class="fas fa-undo"></i> Reset </span> </small>  <br> 

     <div v-show="spin" class="spinner-border ml-auto spinner-border-sm text-primary" role="status" aria-hidden="true"></div> <br>
      <small v-show="incorrect" class="font-weight-bold text-danger"><i class="far fa-times-circle"></i> Username or password incorrect</small> 



    </form>

    



    <!-- LOG IN FORM ENDS   -->   
            
    </div>
            
    </div>


    </div>

   <!-- FOOTER STARTS-->
   <Foot/>
  <!-- FOOTER ENDS-->

        
    </div>
</template>
<script>
import Foot from './footer.vue'
export default {
    name:'Loginpage',
    components:{
        Foot
    },
     data(){
       return{
         incorrect:false,
         email:'',
         password:'',
         getmyJSON:'',
         spin: false,
         isLoggedIn: true
        

       }
     },

     methods: {
       loginPage(){
         if(localStorage.myUsers){
        let checkInfo = this.getmyJSON.find(data => data.email === this.email && data.password === this.password)
           if(checkInfo){
            this.spin = true
            this.incorrect = false
            let Auth = JSON.stringify(this.isLoggedIn)
            localStorage.setItem('AuthKey', Auth)
            setTimeout(()=> this.$router.push({name:'Homeac', params:{id:checkInfo.customerId}}), 3000)
           
          }   
         }
        
          else{
            this.incorrect = true
          }
         },

         resetPassword(){

          this.$router.push({name:'Reset'})
         }

     },


   created(){
  if(localStorage.myUsers){
  this.getmyJSON =JSON.parse(localStorage.myUsers)
  }else{
    this.getmyJSON = ''
  }
   
      
    }


}
</script>
<style>
  #section {
  background-color:#F9FAFB
}  
</style>