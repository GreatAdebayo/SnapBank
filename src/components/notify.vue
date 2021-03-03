<template>
    <div>
      <div class="container-fluid">
          <div class="row  mt-4 mb-5">
        <div class="col text-left"> 
        <i class="fas fa-bell ml-2 text-primary"></i>
        <p class="font-weight-bold text-left ml-2">Messages</p> 


  <ul v-for="(item,index) in getmyJSON" :key="index" v-show="userName == item.lastname" class="list-group list-group-flush">
  <li v-for="(n,index) in item.deposit.slice().reverse()" :key="index" class="list-group-item text-primary"><small><i class="fas fa-download text-primary"></i> {{n.notify}} {{n.date}}</small></li>
   <li v-for="(y,index) in item.credit.slice().reverse()" :key="'A'+ index" class="list-group-item text-primary"><small><i class="fas fa-plus-circle"></i> {{y.notify}} {{y.date}}</small></li>
   <li v-for="(x,index) in item.debit.slice().reverse()" :key="'B'+ index" class="list-group-item text-danger"><small><i class="fas fa-minus-circle"></i>  {{x.notify}} to <span class="font-weight-bold">{{x.accsent}} {{x.date}}</span></small></li>
   <li @click="requests"  class="list-group-item " v-for="(z,index) in item.sentrequest.slice().reverse()" :key="'C' + index"><small class="text-success"><i class="fas fa-sync-alt"></i> {{z.notify}}</small></li>
   <li @click="requests"  class="list-group-item " v-for="(a,index) in item.inrequest.slice().reverse()" :key="'C' + index"><small class="text-info"><i class="fas fa-sync-alt"></i> {{a.notify}} {{a.date}}</small></li>
   <li  v-for="(r,index) in item.accepReq" :key="'R' + index" class="list-group-item"><small class="text-primary"> <i class="fas fa-sync-alt font-weight-bold text-primary"></i> {{r.notify}}</small></li>
    <li v-for="(y,index) in item.accepReq2.slice().reverse()" :key="'M' + index" class="list-group-item"><small class="text-primary"> <i class="fas fa-sync-alt font-weight-bold text-primary"></i> {{y.notify}}</small> </li>
     
      
</ul>

        </div>

          </div>
          
          
          </div> 
    </div>
</template>
<script>
export default {
    name:'Notify',
      data(){
        return{
       getmyJSON:'',
        userName: this.$route.params.id,
        }
    },

    methods: {
       requests(){
          this.$router.push({name:'Myrequest'})

        },
    },


     created(){
      this.getmyJSON =JSON.parse(localStorage.myUsers)
    }
}
</script>
<style lang="">
    
</style>