<template>
    <div>
     <div class="container-fluid"> 
    <div class="row mt-3">      
    <div class="col-8 mx-auto pt-3 pb-5 rounded mb-5" id="section" :class="{trans:load}"> 
    <form class="needs-validation w-100">

    <small class="font-weight-bold">  <i class="fas fa-upload text-primary font-weight-bold"></i>  SNAP TRANSFER PAGE</small>

    <div v-show="max" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> Insufficient Funds</small>
    </div>

    <div v-show="sameAcc" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> You can't send money to yourself</small>
    </div>

    <div v-show="accNotFound" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> Please check to confirm if the account number is correct</small>
    </div>
    
 
    
    

  <!-- @click="useBenefic(n.accNo, n.name) -->
    <div class="text-left">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Account Number</small></label>
    <div class="input-group">
    <input @keyup="verifyAccName" v-model="acc" name="accnumber" type="number" class="form-control" id="validationCustom01" placeholder="Account number" aria-label="Recipient's username" aria-describedby="basic-addon2"> 
    </div>
     <div v-show="verifyName" class="spinner-border ml-3 spinner-border-sm text-dark" role="status" aria-hidden="true"></div>
     <p class="pt-2 font-weight-bold" v-show="showName">{{accName}}</p>
    </div>
     
     <div class="text-left">
    <button class="btn btn-success btn-sm mt-2 font-weight-bold px-2" type="button" data-toggle="collapse" data-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">
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

    <div class="text-left mt-2" @click="saveBene">
       <i class="fas fa-save"></i> <small class="font-weight-bold text-primary"> Save as beneficiary? </small>
    </div>

    <div v-show="savedBen" class="alert alert-info mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> Beneficiary Saved</small>
    </div>

     <div v-show="alreadySaved" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> Beneficiary already Saved</small>
    </div>

     <div v-show="bene" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> You can't save yourself as a beneficiary</small>
    </div>
   
    <br>

   
    
   <button @click.prevent="transfer" class="btn btn-success px-3"> <small class="font-weight-bold"><i class="fas fa-upload text-light font-weight-bold"></i> Transfer </small></button> 
   
    </form>
     </div>
     </div>

      <div class="loader" v-show="load">
      <div class="loadingio-spinner-eclipse-i4v08y3a9vr"><div class="ldio-3egt6o5zk8c">
      <div></div>
      </div></div> 
      
     </div>

     <p class="font-weight-bold text-primary loader" v-show="success"><i class="far fa-check-circle"></i> SUCCESSFUL</p>
     
     
    </div>         
   
   
    </div>
</template>
<script>
export default {
    name:'Transfer',

    data(){
        return{
       userName: this.$route.params.id,
       acc:'',
       getmyJSON:'',
       amount:'',
       max:false,
       moneytransfer:'',
       load: false,
       success:false,
       creditAcc:'',
       accName:'',
       verifyName: false,
       showName: false,
       accNotFound: false,
       beneficiary:'',
       savedBen:false,
       amountRemoved:'',
       sameAcc:false,
       bene:'',
       alreadySaved:''
      
        }
    },



    methods:{
        transfer(){
          let checkAcc = this.getmyJSON.find(data => data.customerId == this.userName)
          if(checkAcc){
          if(parseInt(this.amount) > checkAcc.balance){
               this.max = true
          }else if(checkAcc.acnumber === parseInt(this.acc)){
               this.sameAcc = true
          }
            else if(parseInt(this.amount) <= checkAcc.balance){
            this.max = false
            this.sameAcc = false
            this.amountRemoved = this.amount
            checkAcc.balance = checkAcc.balance - parseInt(this.amountRemoved)
            this.moneytransfer = {amount:parseInt(this.amountRemoved), date:new Date().toLocaleString(), status:'Debit', accsent:this.acc, notify:'You just transferred' +  ' ' + '₦'  + parseInt(this.amountRemoved)}
            checkAcc.debit.push(this.moneytransfer)
            let myJSON = JSON.stringify(this.getmyJSON)
            localStorage.setItem('myUsers', myJSON)
            this.load = true
            setTimeout(()=> this.load = false, 3000)
            setTimeout(()=> this.success = true, 2000)
            setTimeout(()=> this.$router.push({name:'Homeac'}), 3000)
            
            }
          }

             let AddBal = this.getmyJSON.find(data => data.acnumber === parseInt(this.acc))
              if(AddBal && !this.amountRemoved == ""){
              AddBal.balance = AddBal.balance + parseInt(this.amountRemoved)
              this.creditAcc = {amount: parseInt(this.amountRemoved), date:new Date().toLocaleString(), status:'Credit', notify:this.userName + ' ' + 'just sent you' + ' ' + '₦'  + parseInt(this.amountRemoved)}
              AddBal.credit.push(this.creditAcc)
              let myJSON = JSON.stringify(this.getmyJSON)
              localStorage.setItem('myUsers', myJSON)
              

            }
       
    },


    verifyAccName(){
    let verifyAcc = this.getmyJSON.find(data => data.acnumber == parseInt(this.acc))
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


    saveBene(){
      if(this.acc == "" || this.accName == ""){
       this.accNotFound = true

      }else{
        this.accNotFound = false
        let savebenefit = this.getmyJSON.find(data => data.customerId == this.userName)
        let Findbenefit = savebenefit.beneficiary.find(data => data.accNo === this.acc)
        if(this.acc == savebenefit.acnumber){
         this.bene = true
        }else if(Findbenefit){
         this.alreadySaved = true
          this.bene = false
        }
        else if(savebenefit){
        this.alreadySaved = false
        this.bene = false
        this.beneficiary = {name:this.accName, accNo: this.acc}
        savebenefit.beneficiary.push(this.beneficiary)
        let myJSON = JSON.stringify(this.getmyJSON)
        localStorage.setItem('myUsers', myJSON) 
        this.savedBen = true
        setTimeout(()=>   this.savedBen = false, 1000)
      }
      }
      
    
      
       

    },

    useBenefic(value, name){
        this.acc = value
        this.accName = name
        this.showName = true
    }



    
},
created(){
      this.getmyJSON =JSON.parse(localStorage.myUsers)
    }
}

</script>
<style>
    
</style>