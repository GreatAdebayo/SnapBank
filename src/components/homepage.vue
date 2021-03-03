<template>
    <div>
     <!-- NAV BAR STARTS -->
    <nav class="navbar navbar-expand-md bg-light navbar-light fixed-top">
    <router-link to="/" class="navbar-brand"> <h5 class="text-left font-weight-bold text-primary ml-3">
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
    <a class="nav-link text-primary font-weight-bold"><strong><i class="fas fa-lock" @click="login" ></i> Log In</strong></a>
    </li>
    </ul>

    <ul class="navbar-nav mt-3">
    <li class="nav-item ">
    <button class="btn btn-primary  mb-2 px-3 font-weight-bold" @click="create" ><i class="fas fa-plus"></i> Create Account </button>
    </li>
    </ul>

    </div>  
    </nav>
    
   <!-- NAV BAR ENDS -->

    <!-- SECTION 1 STARTS -->
   <section class="home-section">
     <div class="container-fluid"> 
     <div class="row mt-5"> 

     <div class="col-8 mt-5 justify-content-center mb-5 animated fadeIn"> 
     <h5 class="display-4">Your best social  <br> <span class="text-primary font-weight-bold"> payment </span>  platform</h5>
     <button class="btn btn-success font-weight-bold" @click="create"> Create Account <i class="fas fa-arrow-circle-right"></i></button> <br>
     <i class="fab fa-apple fa-3x mt-4 mr-4"></i> <i class="fab fa-google-play fa-2x mt-4"></i>
     </div>

     <div class="col-4 mt-5 text-center animated fadeInRight"> 
     <img src="../assets/mockup.png" class="img-fluid" alt="Responsive image">
     </div>

     </div>
     </div>
     
   </section>
  <!-- SECTION 1 ENDS-->
    

<!-- SECTION 2 STARTS-->
    <section>
    <div class="container-fluid"> 
    <div class="row mt-4 justify-content-left">
    <div class="col-md-4 mb-3  animated fadeInLeft"> 
    <i class="fas fa-certificate fa-2x text-primary mt-2"></i> <p class="font-weight-bold"> Deposit money<br> 
    <span class="text-primary"> seamlessly </span></p>
    </div> 
    <div class="col-md-4 mb-3 animated fadeIn"> 
    <i class="fas fa-money-bill-wave-alt fa-2x text-primary mt-2"></i>   
    <p class="font-weight-bold">Request payments  <span class="text-primary"> from friends </span></p>
    </div> 
    <div class="col-md-4 mb-3 animated fadeInRight"> 
    <i class="fas fa-smile fa-2x text-primary mt-2"></i>    
    <p class="font-weight-bold">Transfer your money <br> <span class="text-primary"> snappy </span></p>
    </div> 

    </div>

    </div>
    </section>
<!-- SECTION 2 ENDS-->

 <!-- SECTION 3 STARTS -->
   <section class="bg-primary">
     <div class="container"> 
     <div class="row mt-5"> 

     <div class="col-md-8 my-5 text-left mx-auto wow animated fadeInLeft"> 
     <h5 class="display-4 text-white font-weight-bold pb-3">Utilize <br> the
      Power of <br> our app</h5>
     <button class="btn btn-success font-weight-bold" @click="create"> Create Account <i class="fas fa-arrow-circle-right"></i></button> 
 
     </div>

     <div class="col-md-4 mt-5 mx-auto wow animated fadeInUp"> 
     <img src="../assets/lap.png" class="img-fluid" alt="Responsive image">
     </div>

     </div>
     </div>
     
   </section>
  <!-- SECTION 3 ENDS-->


  <!-- FOOTER STARTS-->
   <Foot/>
  <!-- FOOTER ENDS-->
    </div>
</template>
<script>
import Foot from './footer.vue'
export default {
    name:'Home',
    components:{
        Foot
    },
    data(){
        return{
           modal: '',
           close: false
        }
    },

    methods:{
        login(){
          this.$router.push({path: '/loginpage'}) 
        },

        create(){
        this.$router.push({path: '/signup'})  
        },
         


        
    },

  
}
</script>

<style>
  .navbar {
  opacity: 0.8;
}
.custom-toggler.navbar-toggler {
  border: none;
  outline: none;
}

.home-section{
    background-color:#F9FAFB ;
}
</style>