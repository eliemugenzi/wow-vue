<template>
<div>
 
  <div class="holder">
    <form @submit.prevent="addSkill">
      <input type="text" placeholder="Enter a skill you have" v-model="skill"  name="skill" v-validate="'min:5'">
      <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
        <p class="alert" v-if="errors.has('skill')" >
        {{errors.first('skill')}}
      </p>
      </transition>
      <input type="checkbox" v-model="checked">
    </form>
    <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
    <ul v-for="(data,index) in skills" :key="index">
        <li>{{data.skill}}</li>
        <i class="fas fa-minus-cirlce" v-on:click="deleteSkill(index)"></i>
    </ul>
    </transition-group>
    <!-- <div v-bind:class="{alert:showAlert}" >Simple alert</div>
    <div v-bind:class="alertObject" >Simple alert</div> -->
  </div>
</div>
</template>

<script>
export default {
  name:'Skills',
  data:()=>{
    return{
      name:'Sequel Pro',
      btnState:false,
      skill:'',
      skills:[
        {skill:'Vue.js'},
        {skill:'Frontend Developer'}
      ],
      showAlert: true,
      alertObject:{
        alert:true
      },
      checked:false
    }
  },
  methods:{
    changeName(){
      this.name="Kwiff";
      this.btnState=true;
    },
    addSkill(){
      this.$validator.validateAll().then(result=>{
        if(result===true){
           this.skills.push({
              skill:this.skill
           });
           this.skill="";
        } else{
          console.log('Not valid');
        }
      });
    },
    deleteSkill(id){
      this.skills.splice(id,1);
    }
  }
}
</script>

<style scoped>
 @import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.10.2/css/all.min.css"; 
  .holder {
    background: #fff;
  }
  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: .8em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }
  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }
  .container {
    box-shadow: 0px 0px 40px lightgray;
  }
  input {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687F7F;
    outline:none; 
  }
  .alert {
    background: #fdf2ce;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }
  .alert-in-enter-active {
    animation: bounce-in .5s;
  }
  .alert-in-leave-active {
    animation: bounce-in .5s reverse;
  }
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
i {
  float:right;
  cursor:pointer;
}
</style>