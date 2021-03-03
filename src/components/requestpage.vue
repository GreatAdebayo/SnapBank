<template lang="">
    <div>
      <div class="container-fluid"> 
    <div class="row mt-3">      
    <div class="col-8 mx-auto pt-3 pb-5 rounded mb-5" id="section" :class="{trans:load}"> 
    <form class="needs-validation w-100">

    <small class="font-weight-bold">  <i class="fas fa-sync-alt text-primary"></i> PAYMENT REQUEST PAGE</small>

   <div v-show="max" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> ₦1000 is the minimum you can request</small>
    </div>

     <div v-show="accNotFound" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> Please check to confirm if the account number is correct</small>
    </div>
     <div v-show="sameAcc" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> You can't request money from yourself</small>
    </div>

    <div class="text-left">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Account Number</small></label>
    <input @keyup="verifyAccName" v-model="acc" name="accnumber" type="number" class="form-control" id="validationCustom01" placeholder="Account number">
    </div> 
    <div class="text-left">
    <div v-show="verifyName" class="spinner-border ml-3 spinner-border-sm text-dark" role="status" aria-hidden="true"></div> 
    
     <p class="font-weight-bold mt-2" v-show="showName">{{accName}}</p>
    </div>

     <div class="text-left">
    <button class="btn btn-dark btn-sm mt-2 font-weight-bold px-2" type="button" data-toggle="collapse" data-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">
    Beneficiaries
    </button>
     </div>
    <div class="collapse" id="collapseExample">
    <div class="card card-body">
    <ul class="list-group-flush justify-content-center" v-for="(item,index) in getmyJSON" :key="index" v-show="userName == item.customerId">
    <li @click="useBenefic(n.accNo, n.name)"  v-for="(n,index) in item.beneficiary" :key="'A' + index" class="list-group-item"><small class="text-primary font-weight-bold">{{n.name}} {{n.accNo}}</small></li>
    </ul>

     </div>
    </div>


    <div class="text-left mt-3">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Amount</small></label>
    <input v-model="amount" name="amt" type="text" class="form-control" id="validationCustom01" placeholder="Amount"  required>
 
    </div>

    <div class="text-left mt-3">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Remarks (optional)</small></label>
    <input name="firstname" type="text" class="form-control" id="validationCustom01" placeholder="Remarks">
    </div>

    <br>
    
   <button @click.prevent="request" class="btn btn-dark px-3"> <small class="font-weight-bold"><i class="fas fa-sync-alt"></i> Send Request </small></button> 
   
    </form>
    <div id="accordion">
  <div class="card mt-4">
    <div class="card-header" id="headingOne">
      <h5 class="mb-0">
        <button class="btn" data-toggle="collapse" data-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
        <small class="font-weight-bold"><i class="fas fa-share-square text-primary"></i> Sent Requests</small>
        
        </button>
      </h5>
    </div>

    <div id="collapseOne" class="collapse show" aria-labelledby="headingOne" data-parent="#accordion">
      <div class="card-body">
      <ul v-for="(item,index) in getmyJSON" :key="'C'+index" v-show="userName == item.customerId" class="list-group">
      <li v-for="(y,index) in item.sentrequest.slice().reverse()" :key="'B' + index" class="list-group-item"><small class="text-primary"> <i class="fas fa-sync-alt font-weight-bold text-primary"></i> {{y.notify}}</small> </li>
        </ul>
        </div>
    </div>
  </div>
  <div class="card">
    <div class="card-header" id="headingTwo">
      <h5 class="mb-0">
        <button class="btn collapsed" data-toggle="collapse" data-target="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">
           <small class="font-weight-bold"><i class="fas fa-share-square text-primary"></i> Your Requests Status</small>
       
        </button>
      </h5>
    </div>
    <div id="collapseTwo" class="collapse" aria-labelledby="headingTwo" data-parent="#accordion">
      <div class="card-body">
        <ul v-for="(item,index) in getmyJSON" :key="'A'+index" v-show="userName == item.customerId" class="list-group">
      <li v-for="(y,index) in item.accepReq2.slice().reverse()" :key="'M' + index" class="list-group-item"><small class="text-primary"> <i class="fas fa-sync-alt font-weight-bold text-primary"></i> {{y.notify}}</small> </li>
        </ul></div>
    </div>
  </div>
  </div>
   
     </div> 
     </div>

   

      <div class="loader" v-show="load">
      <div class="loadingio-spinner-eclipse-i4v08y3a9vr"><div class="ldio-3egt6o5zk8c">
      <div></div>
      </div></div> 
      
     </div>

     <p class="font-weight-bold text-primary loader" v-show="success"><i class="far fa-check-circle"></i> REQUEST SENT</p>
     
     
    </div>         
    <!-- LOG IN FORM ENDS   -->
     
    </div>
</template>
<script>
export default {
    name:'Request',
    data(){
        return{
        getmyJSON:'',
        userName: this.$route.params.id,
        acc:'',
        accNotFound:'',
        accName:'',
        verifyName:'',
        showName :'',
        amount:'',
        sentReq:'',
        inReq:'',
        load:'',
        success:'',
        sameAcc:''
        }
    },
    methods: {
    verifyAccName(){
    let verifyAcc = this.getmyJSON.find(data => data.acnumber === parseInt(this.acc))
    if(verifyAcc){
    this.accNotFound = false
    this.accName = verifyAcc.firstname + ' ' + verifyAcc.lastname + ' ' + verifyAcc.middlename    
    this.verifyName = true
    setTimeout(()=>  this.verifyName = false, 2000)
    setTimeout(()=>  this.showName = true, 2000)
      }
      else{
        this.accNotFound = true
        this.showName = false
      }
    },



    request(){
        let yourRequest = this.getmyJSON.find(data => data.customerId == this.userName)
        let sendRequest = this.getmyJSON.find(data => data.acnumber === parseInt(this.acc))
        if(parseInt(this.acc) === yourRequest.acnumber){
         this.sameAcc = true
        }else if(sendRequest){
          this.sameAcc = false
        this.inReq = {amount:parseInt(this.amount), date:new Date().toLocaleString(), notify:this.userName + ' ' + 'requested' + ' ' + '₦'  + parseInt(this.amount), name:this.userName}  
        sendRequest.inrequest.push(this.inReq)
        let myJSON = JSON.stringify(this.getmyJSON)
        localStorage.setItem('myUsers', myJSON)
        this.load = true
        setTimeout(()=> this.load = false, 3000)
        setTimeout(()=> this.success = true, 2000)
        setTimeout(()=> this.$router.push({name:'Homeac'}), 3000)
        }

        if(yourRequest){
        this.sentReq = {notify:'You just sent a request of' + ' ' + '₦'+parseInt(this.amount) + ' ' + new Date().toLocaleString() + ' ' + 'to'+ ' ' +sendRequest.lastname, status:'Pending'}
        yourRequest.sentrequest.push(this.sentReq)
        let myJSON = JSON.stringify(this.getmyJSON)
        localStorage.setItem('myUsers', myJSON)

        }
    },

      useBenefic(value, name){
        this.acc = value
        this.accName = name
        this.showName = true
    },

 

       
    },

 created(){
      this.getmyJSON =JSON.parse(localStorage.myUsers)
    }
    
}
</script>
<style lang="">
    
</style>