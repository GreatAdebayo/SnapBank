<template>
    <div>
      <!-- NAV BAR STARTS -->
    <nav class="navbar navbar-expand-md bg-light navbar-light fixed-top">
    <a @click="home" class="navbar-brand"> <h5 class="text-left font-weight-bold text-primary ml-3">
    <i class="fas fa-poo-storm"></i> SnapBank</h5>
    </a>
    <button class="navbar-toggler custom-toggler" type="button" data-toggle="collapse" 
    data-target="#collapsibleNavbar" aria-controls="collapsibleNavbar" aria-expanded="false" 
    aria-label="Toggle navigation">
    <span class=" navbar-toggler-icon "></span>
    </button>
    <div class="collapse navbar-collapse" id="collapsibleNavbar">

    <ul class="navbar-nav ml-auto mr-2 px-5 text-center">
        <li class="nav-item pt-2">
    <a @click=" deposit"  class="nav-link text-primary font-weight-bold"><strong><i class="fas fa-download"></i> Deposit</strong></a>
    </li>

    <li class="nav-item pt-2">
    <a @click="transfer" class="nav-link text-primary font-weight-bold" ><strong> Quick Transfer <i class="fas fa-upload"></i></strong></a>
    </li>
    </ul>

    <ul class="navbar-nav mt-3">
    <li class="nav-item ">
    <button  class="btn btn-primary  mb-2 px-3 font-weight-bold" data-toggle="modal" data-target="#exampleModal" > <i class="fas fa-unlock"></i> Log Out </button>
    </li>
    </ul>

    </div>  
    </nav>
    
   <!-- NAV BAR ENDS -->  


   <section v-for="(item,index) in getmyJSON" :key="index" v-show="userName == item.customerId">
    <div class="container-fluid">
            
   <div class="row mt-5">
    <div class="col-10 mt-5">
    <p class="font-weight-bold text-left ml-2"><i class="fas fa-user text-primary"></i> {{item.lastname}}  {{item.acnumber}} <i class="far fa-copy"></i><br>  <small class="font-weight-bold color">Hello, wash your hands <i class="fas fa-sign-language"></i></small></p>
    </div>
    <div class="col-2 mt-5"  @click="notify">
   <i class="fas fa-bell"></i> <br>
   
    <a class="badge badge-primary">Message</a>
    </div>
   </div>

   </div>
   <div class="container">
      <div class="row">     
    <div class="col-md mt-2 border rounded-right  bg-primary ml-1 mr-2 text-white animated fadeInLeft">
    <p class="font-weight-bold text-left pt-2"><i class="fas fa-shield-alt"></i> Account Balance NGN </p>
    <h5 class="text-left ml-4 mb-2 font-weight-bold"> ₦{{item.balance}}</h5>
     

     
    </div>

     <div class="col-sm  mt-2 border  rounded-left bg-dark ml-1 mr-2 text-white animated fadeIn">
    <p class="font-weight-bold text-left pt-2"><i class="fas fa-shield-alt"></i> USD </p>
    <h5 class="text-left ml-4 mb-2 font-weight-bold"> ${{item.balance/381}}</h5>

     
    </div>

     <div class="col-md mt-2 border rounded-right  bg-success ml-1 mr-2 text-white animated fadeInRight">
    <p class="font-weight-bold text-left pt-2"><i class="fas fa-shield-alt"></i>  EURO </p>
    <h5 class="text-left ml-4 mb-2 font-weight-bold"> €{{item.balance/450}}</h5>
    
     
    </div>

    </div>

   </div>  

   </section>

 

    <section class="mb-5">
    <router-view> </router-view>
    </section>
 






  



      <!-- FOOTER STARTS -->
   <div class="row bg-light nav fixed-bottom mt-3 d-flex">
   <div class="col pt-2" @click="home">
     <i class="fas fa-home text-dark"></i> <br>
   <small class="font-weight-bold text-dark">Home </small>
   </div>


   <div class="col pt-2" @click="acchistory">
    <i  class="fas fa-history text-dark"></i>  <br>
   <small  class="font-weight-bold text-dark">History</small>
   </div>

    <div class="col pt-2" @click="deposit">
    <i class="fas fa-download text-dark"></i><br>
   <small class="font-weight-bold text-dark"> Fund</small>
   </div>

    <div class="col pt-2"  @click="transfer">
   <i class="fas fa-upload text-dark font-weight-bold"></i> <br>
   <small class="font-weight-bold text-dark"> SnapPay</small>
   </div>

   <div class="col pt-2" @click="request">
   <i class="fas fa-sync-alt text-dark"></i> <br>
   <small class="font-weight-bold "> Request</small>
   </div>

  <div class="col pt-2"  @click="profile">
   <i class="fas fa-user-circle text-dark"></i><br>
   <small class="font-weight-bold text-dark"> Profile</small>
   </div>

 

  
  </div>
    <!-- FOOTER ENDS -->
     
     <!-- LOG OUT MODAL -->
   <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
      <h5 class="text-center font-weight-bold text-primary ml-3">
    <i class="fas fa-poo-storm"></i> SnapBank</h5>
    
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
       <p class="font-weight-bold"><i class="fas fa-info-circle"></i> Are you sure you want to Log out?</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary btn-sm font-weight-bold" data-dismiss="modal"><i class="far fa-thumbs-up"></i> Continue Banking</button>
        <button @click="logOut" type="button" class="btn btn-danger btn-sm font-weight-bold" data-dismiss="modal"><i class="far fa-sad-tear"></i> Yes</button>
      </div>
    </div>
  </div>
</div>

<!-- LOG OUT MODAL -->
    </div>
</template>
<script>
export default { 
    name: 'Account',

    data(){
   return{
      userName: this.$route.params.id,
      getmyJSON:'',
      response: Object,
      rate:'',
      AuthKey:''
   }
    },

    methods: {

        transfer(){
          this.$router.push({name:'Transfer'})
        },
        profile(){
           this.$router.push({name:'Profile'})
        },
        deposit(){
          this.$router.push({name:'Deposit'})
        },
        home(){
          this.$router.push({name:'Homeac'})
        },
        notify(){
          this.$router.push({name:'Notify'})

        },
         acchistory(){
          this.$router.push({name:'Acchistory'})

        },

        request(){
            this.$router.push({name:'Request'})
        },

     

        logOut(){
        this.AuthKey = false
        let myJSON = JSON.stringify(this.AuthKey)
        localStorage.setItem('AuthKey', myJSON)
        this.$router.push({name:'Home'})
        }

        
        
        
    },

    

     created(){
    this.getmyJSON =JSON.parse(localStorage.myUsers),
    this.AuthKey =JSON.parse(localStorage.AuthKey),
    window.axios.get("https://currency-converter5.p.rapidapi.com/currency/list").then(resp =>{
       if (resp.status == 200){
       this.response = resp.data;
      
         console.log(this.response)
           }
            })
    },
    

}
</script>
<style>
  .color{
      color:#888888
  } 
  .nav{
      opacity: 0.8;
  } 

 
</style>