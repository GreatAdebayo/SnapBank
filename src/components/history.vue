<template>
   <div>
    <div class="container-fluid color"> 
    <div class="row mt-4">
    <div class="col-10 mx-auto">
    <p class="font-weight-bold"><i class="fas fa-history text-primary"></i> Account History</p>
    </div>
    </div>
    
     <div class="row mt-3">
     <div class="col-md-5 mx-auto">
     <p class="font-weight-bold text-danger"><i class="fas fa-minus-circle"></i> DEBIT</p>
     <ul v-for="(item,index) in getmyJSON" :key="index" v-show="userName == item.customerId" class="list-group list-group-flush justify-content-center text-primary">
     <li  v-for="(n,index) in item.debit.slice().reverse()" :key="'B' + index" class="list-group-item"><small class="text-danger">{{n.notify}} to {{n.accsent}}<br> {{n.date}}</small> <small class="font-weight-bold text-danger">{{n.status.toUpperCase()}}</small></li>
      <li  v-for="(r,index) in item.accepReq.slice().reverse()" :key="'A' + index" class="list-group-item"><small class="text-danger"> <i class="fas fa-sync-alt font-weight-bold text-danger"></i> {{r.notify}}</small></li>
      
     </ul>
     </div>

     <div class="col-md-5 mt-2 mx-auto">
     <p class="font-weight-bold text-primary"><i class="fas fa-plus-circle"></i> CREDIT~DEPOSIT</p>
     <ul v-for="(item,index) in getmyJSON" :key="index" v-show="userName == item.customerId" class="list-group list-group-flush justify-content-center text-primary">
     <li class="list-group-item" v-for="(n,index) in item.credit.slice().reverse()" :key="'A' + index"><small>{{n.notify}}  <br> {{n.date}}</small> <small class="text-primary font-weight-bold">{{n.status.toUpperCase()}} </small> </li>
     <li class="list-group-item" v-for="(y,index) in item.deposit.slice().reverse()" :key="'B'+ index"><small>₦{{y.amount}} {{y.date}}</small> <small class="text-primary font-weight-bold">{{y.status.toUpperCase()}} </small> </li>
     <li v-for="(y,index) in item.accepReq2.slice().reverse()" :key="'M' + index" class="list-group-item"><small class="text-primary"> <i class="fas fa-sync-alt font-weight-bold text-primary"></i> {{y.notify}}</small> </li>
      
     </ul>
     </div>
    
   </div>

    </div>
   </div>
</template>
<script>
export default {
    name:'Acchistory',

     data(){
     return{
        userName: this.$route.params.id,
        getmyJSON:'',
        searchAmt:'',
        transHis:'',
       
         }
     },


     
    created(){
      this.getmyJSON =JSON.parse(localStorage.myUsers)
    }
    
}
</script>
<style>
    
</style>