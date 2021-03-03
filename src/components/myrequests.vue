<template>
    <div>
      <div class="container-fluid">
    <div class="row mt-4">
        <div class="col-8 mx-auto">
        <div v-show="accept" class="alert alert-success" role="alert">
      <small class="font-weight-bold"> Accepted </small>
     </div>  
      <div v-show="insufficient" class="alert alert-danger" role="alert">
      <small class="font-weight-bold"> Insufficient Funds </small>
     </div>  
      <ul v-for="(item,index) in getmyJSON" :key="index" v-show="userName == item.customerId" class="list-group">
       <p  v-show="item.inrequest.length > 0" class="font-weight-bold text-center"><i class="fas fa-edit text-primary"></i> Pending requests from friends</p>
     
       <li  v-for="(n,index) in item.inrequest" :key="'A' + index" class="list-group-item"><small class="text-primary"> <i class="fas fa-sync-alt font-weight-bold text-primary"></i> {{n.notify}} {{n.date}} <i @click="Accept(n.name, n.amount, item.inrequest, index)" class="fas fa-vote-yea ml-2 text-success"></i> <i @click="cancelReq(item.inrequest, index)" class=" ml-2 text-danger far fa-window-close"></i> </small>
       </li>
       
        </ul>

       <ul v-for="(item,index) in getmyJSON" :key="'C' +index" v-show="userName == item.customerId" class="list-group mt-5">
       <p  v-show="item.accepReq.length > 0" class="font-weight-bold text-center"><i class="fas fa-check text-primary"></i> Accepted Requests from friends</p>
     
       <li  v-for="(n,index) in item.accepReq.slice().reverse()" :key="'A' + index" class="list-group-item"><small class="text-primary"> <i class="fas fa-sync-alt font-weight-bold text-primary"></i> {{n.notify}}</small>
       </li>
       
        </ul>
        </div>
       </div>
          
    </div>  
    </div>
</template>
<script>
export default {
    name:'MyRequest',
    data(){
        return{
        getmyJSON:'',
        userName: this.$route.params.id,
        amountRemoved:"",
        accept: false,
        insufficient: false,
        acceptRequest:'',
        acceptRequest2:''
       
        }
    },

    methods: {
        Accept(name, amount, item, index){
        let getBalance = this.getmyJSON.find(data => data.customerId == this.userName)
          if(getBalance){
          if(amount > getBalance.balance){
             this.insufficient = true
             setTimeout(()=>  this.insufficient = false, 1000)
          } else if(amount <= getBalance.balance){
              this.amountRemoved = amount
              getBalance.balance = getBalance.balance - this.amountRemoved
              this.acceptRequest = {notify: 'You just accepted the payment of' + ' '+  '₦'+this.amountRemoved + ' ' + 'from' + ' ' + name + ' ' + new Date().toLocaleString()}
              getBalance.accepReq.push(this.acceptRequest)
              let myJSON = JSON.stringify(this.getmyJSON)
              localStorage.setItem('myUsers', myJSON)             
          }

        }

        let AddBal = this.getmyJSON.find(data => data.customerId == name)
        if(AddBal && !this.amountRemoved == ""){
        AddBal.balance = AddBal.balance + this.amountRemoved
        this.acceptRequest2 = {notify:'Your request of' + ' '+ '₦'+this.amountRemoved +' ' + ' to' + ' '+ this.userName + ' ' + 'has been accepted on' + ' ' + new Date().toLocaleString()}
        AddBal.accepReq2.push(this.acceptRequest2)
        this.accept = true
        setTimeout(()=>  this.accept=false, 1000)
        item.splice(index, 1)
        let myJSON = JSON.stringify(this.getmyJSON)
        localStorage.setItem('myUsers', myJSON)    

        }
        
        },

        cancelReq(item, index){
         item.splice(index, 1)
        let myJSON = JSON.stringify(this.getmyJSON)
        localStorage.setItem('myUsers', myJSON) 
        

        }
    },


     created(){
      this.getmyJSON =JSON.parse(localStorage.myUsers)
    }
}
</script>
<style>
    
</style>