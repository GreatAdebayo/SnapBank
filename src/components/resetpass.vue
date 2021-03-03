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
     <small class="font-weight-bold ml-3"><i class="fas fa-user-circle text-primary"></i> PASSWORD RESET</small>
   
    <div class="text-left text-primary">
    <label for="validationCustom01"><small class="font-weight-bold"><i class="fas fa-user"></i>  Email </small></label>
    <input  v-model="email" name="email" type="email" class="form-control" id="validationCustom08" placeholder="email">
    </div> <br>

    <div class="text-left text-primary" v-show="showNewpwd">
    <label for="validationCustom02"><small class="font-weight-bold"><i class="fas fa-unlock"></i> New Password</small></label>
    <input v-model="password" name="password" type="password" class="form-control" id="validationCustom09" placeholder="password">
   
     </div>
   
     
     <button @click.prevent="checkemail"  v-show="showemail" class="btn btn-primary btn-sm  mt-3 px-4"> <small class="font-weight-bold"> PROCEED </small> </button> <br>
     <button @click.prevent="resetPassword"  v-show="showNewpwd" class="btn btn-primary btn-sm  mt-3 px-4"> <small class="font-weight-bold"> RESET <i  class="fas fa-undo"></i> </small> </button> <br>
   
    <small v-show=" emailNotFound" class="font-weight-bold text-danger"><i class="far fa-times-circle"></i> Email not found in our system</small> 

    <div v-show="spin" class="spinner-border ml-auto spinner-border-sm text-primary" role="status" aria-hidden="true"></div> <br>
      <small v-show="success" class="font-weight-bold text-primary"> Password Successfully Changed</small> 


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
    name:'Reset',
      components:{
        Foot
    },

    data(){
        return{
       getmyJSON:'',
       email:'',
       showNewpwd: false,
       emailNotFound:false,
       password:'',
       spin:false,
       success:false,
       showemail: true
        }
    },

    methods:{
        checkemail(){
        let checkInfo = this.getmyJSON.find(data => data.email === this.email)
        if(checkInfo){
         this.showNewpwd = true
         this.showemail = false
         this.emailNotFound = false
         }
          else{
              this.emailNotFound = true
          }

        },

        resetPassword(){
        let checkInfo = this.getmyJSON.find(data => data.email === this.email)  
        if(checkInfo){
         checkInfo.password = this.password
        let myJSON = JSON.stringify(this.getmyJSON)
        localStorage.setItem('myUsers', myJSON)
        this.spin = true
        setTimeout(()=> this.spin = false, 3000)
        setTimeout(()=> this.success = true, 3000)
        setTimeout(()=> this.$router.push({name:'Login'}), 4000)  
          }
        }
    },

    created(){
   this.getmyJSON =JSON.parse(localStorage.myUsers)
      
    }
}
</script>
<style lang="">
    
</style>