<template>
    <div>
     <div class="container-fluid"> 
    <div class="row mt-3">      
    <div class="col-8 mx-auto pt-3 pb-5 rounded mb-5" id="section" :class="{trans:load}"> 
    <form class="needs-validation w-100" novalidation>

    <small class="font-weight-bold"> <i   class="fas fa-download text-primary"></i> FUND DEPOSIT PAGE</small>

    <div v-show="depo" class="alert alert-danger mt-2" role="alert">
    <small class="font-weight-bold"><i class="fas fa-info-circle"></i> You can not deposit below  ₦1000</small>
    </div>

   

    <div class="text-left mt-3">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Amount</small></label>
    <input v-model="amount" name="amount" type="number" class="form-control" id="validationCustom01" placeholder="Amount">
   
    </div>

  


    <div class="text-left mt-3">
    <label for="validationCustom01"><small class="text-primary font-weight-bold">Remarks (optional)</small></label>
    <input name="remarks" type="text" class="form-control" id="validationCustom01" placeholder="Remarks">
    </div> <br>
    
   <button @click.prevent="deposit" class="btn btn-success px-3"> <small class="font-weight-bold"><i class="fas fa-download text-light"></i> Deposit </small></button> 
   
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
    <!--DEPOSIT FORM ENDS   -->
   
    </div>
</template>
<script>
export default {
    name:'Deposit',
    data(){
        return{
            getmyJSON:'',
            userName: this.$route.params.id,
            amount:null,
            depo:false,
            moneydeposit:'',
            load: false,
            success:false
        }
    },

    methods:{
        deposit(){
        let checkBal = this.getmyJSON.find(data => data.customerId == this.userName)
        if(checkBal && this.amount < 1000){
             this.depo = true
        } 
       else{
        this.depo = false
        checkBal.balance += parseInt(this.amount)
        this.moneydeposit = {amount:parseInt(this.amount), date:new Date().toLocaleString(), status:'Deposit', notify:'You have successfully deposited' + ' ' + '₦'  + parseInt(this.amount)}
        checkBal.deposit.push(this.moneydeposit)
        let myJSON = JSON.stringify(this.getmyJSON)
        localStorage.setItem('myUsers', myJSON)
        this.load = true
        setTimeout(()=> this.load = false, 3000)
        setTimeout(()=> this.success = true, 2000)
        setTimeout(()=> this.$router.push({name:'Homeac'}), 3000)
         
       }
        } 
        },
    






 created(){
      this.getmyJSON =JSON.parse(localStorage.myUsers)
    }
    
}


</script>
<style>

@keyframes ldio-3egt6o5zk8c {
  0% { transform: rotate(0deg) }
  50% { transform: rotate(180deg) }
  100% { transform: rotate(360deg) }
}
.ldio-3egt6o5zk8c div {
  position: absolute;
  animation: ldio-3egt6o5zk8c 1s linear infinite;
  width: 160px;
  height: 160px;
  top: 20px;
  left: 20px;
  border-radius: 50%;
  box-shadow: 0 4px 0 0 #007bff;
  transform-origin: 80px 82px;
}
.loadingio-spinner-eclipse-i4v08y3a9vr {
  width: 200px;
  height: 200px;
  display: inline-block;
  overflow: hidden;
  background: none;
}
.ldio-3egt6o5zk8c {
  width: 100%;
  height: 100%;
  position: relative;
  transform: translateZ(0) scale(1);
  backface-visibility: hidden;
  transform-origin: 0 0; /* see note above */
}
.ldio-3egt6o5zk8c div { box-sizing: content-box; }

.loader{
  position: fixed;
  z-index: 99;
  top:0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

}  

.trans{
    opacity: 0.4;
}
</style>