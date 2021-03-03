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
    <a class="nav-link text-light font-weight-bold"><strong><i class="fas fa-lock" @click="login" ></i> Log In</strong></a>
    </li>
    </ul>

    <ul class="navbar-nav mt-3">
    <li class="nav-item ">
    <button class="btn btn-light text-primary  mb-2 px-3 font-weight-bold" > Sign up </button>
    </li>
    </ul>

    </div>  
    </nav>
    
   <!-- NAV BAR ENDS --> 


   <!-- LOG IN FORM STARTS    -->
    <div class="container-fluid"> 
    <div class="row mt-5">      
    <div class="col-8 mx-auto  p-5 mt-5 rounded" id="section"> 
    <h5 class="text-center font-weight-bold text-primary ml-3">
    <i class="fas fa-poo-storm"></i> SnapBank</h5>


    <form class="needs-validation w-100" @submit.prevent="createUserAccount">
    <small class="font-weight-bold"><i class="fas fa-user-circle text-primary"></i> ACCOUNT CREATION PAGE</small>

    <div v-if="errors.length" class="alert alert-danger mt-2" role="alert">
    <small v-for="(error, index) in  errors"
    :key="index" class="font-weight-bold"><i class="fas fa-info-circle"></i> {{error}} <br></small> 
    </div>  
     
    <div v-show="emailexist" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> Email address or Phone Number already used, please provide a new one </small>
    </div>
    

    <div class="form-row w-100 mt-4">
    <div class="col-md-6 mb-3 text-left">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">First name</small></label>
    <input v-model="user.firstname"   name="firstname" type="text" class="form-control"  placeholder="First name">
    </div>
    <div class="col-md-6 mb-3 text-left">
    <label for="validationCustom02"><small class="text-primary font-weight-bold">Last name</small></label>
    <input v-model="user.lastname" name="lastname" type="text" class="form-control"  placeholder="Last name">
    <div class="invalid-feedback">
     Please provide your last name
     </div>
     </div>
     </div>


     <div class="form-row">
    <div class="col-md-7 mb-3 text-left text-primary font-weight-bold">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Middle name</small></label>
    <input v-model="user.middlename"  name="midname" type="text" class="form-control"  placeholder="Middle name">
    <div class="invalid-feedback">
    Please provide your middlename
    </div>
    </div>
    <div class="col-md-5 mb-3 text-left text-primary font-weight-bold">
    <label for="validationCustom02"><small class="text-primary font-weight-bold">Date of birth</small></label>
    <input  v-model="user.dob"  name="dob" type="date" class="form-control"  placeholder="DOB">
     </div>
     </div>

     <div class="form-row">
    <div class="col-md-8 mb-3 text-left text-primary font-weight-bold">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Mobile</small></label>
    <input v-model="user.mobile" name="phone" type="number" class="form-control"  placeholder="phone number">
    
    </div>
    <div class="col-md-4 mb-3 text-left text-primary font-weight-bold">
    <label for="validationCustom02"><small class="text-primary font-weight-bold">Gender</small></label>
      <select  name="gender" v-model="user.selected" class="form-control">
      <option disabled value="">Please select your gender</option>
      <option>Male</option>
      <option>Female</option>
    </select>
     </div>
     </div>

    <div class="form-row">
    <div class="col-md-6 mb-3 text-left">
    <label for="validationCustom01"><small class=" text-primary font-weight-bold"><i class="fas fa-user"></i> Email</small></label>
    <input  v-model="user.email" name="email" type="email" class="form-control"  placeholder="email">
   
    </div>
    <div class="col-md-6 mb-3 text-left">
    <label for="validationCustom02"><small class="text-primary font-weight-bold"><i class="fas fa-unlock"></i> Password</small></label>
    <input  v-model="user.password" name="password" type="password" class="form-control" placeholder="password">
     </div>
     </div>
   <button class="btn btn-success px-4"><i class="fas fa-plus"></i> <small class="font-weight-bold"> Create </small></button> 
   
    <small class="ml-3 font-weight-bold">Already have an account? <span class="text-primary" @click="login"> <i class="fas fa-sign-out-alt"></i> Log In </span> </small> 
   
    </form>
     </div>
     </div>
     
    </div>         
    <!-- LOG IN FORM ENDS   -->



     <!-- FOOTER STARTS-->
     <Foot/>
     <!-- FOOTER ENDS-->  

        
    </div>
</template>
   <script>
   //    <<<<< VANILLA JAVASCRIPTS STARTS:(to stop the array from being empty on page reload) >>>>>
            let users
            if (localStorage.myUsers) {
            users = JSON.parse(localStorage.myUsers);
            } else {
           users = [];
 
           
            }
  // /     / <<<<< VANILLA JAVASCRIPTS STARTS >>>>>
   import Foot from './footer.vue'
   export default {
    name:'Sign',
    components:{
       Foot
    },
       data(){
         return{
           errors: [],
           user:{
             firstname:null,
             lastname: null,
             middlename:null,
             dob:null,
             mobile:null,
             selected: null,
             email:'',
             password:null,
             balance:0,
             acnumber:null,
             debit:[],
             credit:[],
             deposit:[],
             notify:[],
             sentrequest:[],
             inrequest:[],
             beneficiary:[],
             accepReq:[],
             accepReq2:[],
             customerId:null
            },
            users:users,
            getmyJSON: '',
            emailexist: false,
           
           
         }
       },
        methods: {
         createUserAccount(){
        if(localStorage.myUsers){
        let checkemail = this.getmyJSON.find(data => data.email === this.user.email || data.mobile === this.user.mobile) 
          if(checkemail){
             this.emailexist = true
          } else if(!checkemail || this.user.firstname && this.user.lastname && this.user.middlename && this.user.dob 
          && this.user.mobile && this.user.selected && this.user.email && this.user.password){
           this.user.acnumber = Math.floor(Math.random()* 899999 + 1000000000)
           this.user.customerId = Math.floor(100000 + Math.random() * 900000) 
            this.users.push(this.user)
            let myJSON = JSON.stringify(this.users)
            localStorage.setItem('myUsers', myJSON)
            this.emailexist = false
            this.$router.push({name:'Setup', params:{id:this.user.lastname.toLowerCase()}}) 
           
          }}
          else if (!localStorage.myUsers){
          if(this.user.lastname && this.user.middlename && this.user.dob 
          && this.user.mobile && this.user.selected && this.user.email && this.user.password){
           this.user.acnumber = Math.floor(Math.random()* 899999 + 1000000000)
           this.user.customerId = Math.floor(100000 + Math.random() * 900000) 
            this.users.push(this.user)
            let myJSON = JSON.stringify(this.users)
            localStorage.setItem('myUsers', myJSON)
            this.emailexist = false
            this.$router.push({name:'Setup', params:{id:this.user.lastname.toLowerCase()}}) 

            }
          }

      
         
           


     // <==== FORM VALIDATION ===>
       this.errors = [];

       if (!this.user.firstname) {
        this.errors.push("Firstname required.");
       }
       if (!this.user.lastname) {
        this.errors.push('Lastname required.');
      }
            if (!this.user.middlename) {
        this.errors.push('Middlename required.');
      }

       if (!this.user.dob) {
        this.errors.push('Date of birth required.');
      }
        if (!this.user.mobile) {
        this.errors.push('Phone no required.');
      }
          if (!this.user.selected) {
        this.errors.push('Gender required.');
      }

          if (!this.user.email) {
        this.errors.push('Email required.');
      }

      if (!this.user.password) {
        this.errors.push('Password required.');
      }
       // <==== FORM VALIDATION ===>
     },


    
     login(){
      this.$router.push({path: '/loginpage'})  
        },

     
         
       
    },

  created(){
    if(localStorage.myUsers){
    this.getmyJSON =JSON.parse(localStorage.myUsers)
    }
    else{
      this.getmyJSON = ''
    }
   
  
     
    }
 
    
    }
</script>
<style>
    
</style>