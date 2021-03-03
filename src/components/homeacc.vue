<template>
    <div>
   <section>
  <div class="container-fluid color">
  <div class="row">  
  <div class="col-md mt-5 ml-2 animated fadeInUp">
   <p @click="requests" class="font-weight-bold text-left ml-5"><i class="fas fa-money-bill-wave-alt text-primary"></i> PAYMENT REQUESTS FROM FREINDS</p>
   
  <h5 class="display-4 text-primary font-weight-bold pb-3 mt-5"> <i class="fas fa-credit-card"></i> Apply for  <br> debit cards</h5>
     <button  @click="cardApply" class="btn btn-success font-weight-bold px-4">Apply <i class="fas fa-arrow-circle-right"></i></button> 
 


    <img src="../assets/wall.jpg" class="img-fluid mx-auto mt-4 mb-3 rounded animated fadeInLeft" alt="Responsive image">
    <small class="font-weight-bold"><i class="fas fa-fighter-jet text-primary"></i> Snap Transactions on our WebApp</small>
   </div>

  <div class="col-md mt-5  animated fadeInUp">
 
  <p class="font-weight-bold text-center"><i class="fas fa-arrow-circle-down text-primary"></i> Download our mobile app</p>
  <img src="../assets/mockup.png" class="img-fluid ml-5" alt="Responsive image">
 
      
  </div>





  </div>





  </div>



   </section>


    <!-- SECTION 3 STARTS -->
   <section class="bg-primary">
     <div class="container"> 
     <div class="row mt-2"> 

     <div class="col-md-8 my-5 text-left mx-auto"> 
     <h5 class="display-4 text-white font-weight-bold pb-3">Check our <br>loan offers</h5>
     <button class="btn btn-success font-weight-bold px-4 ml-5">Loan <i class="fas fa-arrow-circle-right"></i></button> 
 
     </div>

     <div class="col-md-4 mt-5 mx-auto"> 
     <img src="../assets/lap.png" class="img-fluid" alt="Responsive image">
     </div>

     </div>
     </div>
    
   </section>
  <!-- SECTION 3 ENDS-->

      
    </div>
</template>
<script>
export default {
    name: 'Homeacc',

    methods:{
     cardApply(){
    this.$router.push({name:'Applycard'})
      },

     requests(){
      this.$router.push({name:'Myrequest'})

        },
    }
  
}
</script>
<style lang="">
 
</style>