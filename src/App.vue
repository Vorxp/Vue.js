<template>
<section id="banner" class="mb-5">
    <nav class="navbar navbar-expand-lg bg-success-subtle shadow-sm fixed-top">
      <div class="col "> Portfolio ของ นายวรพล บุญราศรี 6530200428
      </div>
    </nav>
  </section>


  <section id="home" class="container mt-5 pt-5">
    <div class="row align-items-center">
      
      <div class="col-lg-5 text-center">
        <img src="./assets/Picture.jpg" height="450" class="img" />
      </div>

      <div class="col-lg-6">
        <div class="display-1">Portfolio!</div>
        <div class="display-5 text-success">Vorapol Boonrasri</div>
        <button class="btn btn-secondary mx-1" @click="toggleProfile()"> 
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-person-fill" viewBox="0 0 16 16">
          <path d="M3 14s-1 0-1-1 1-4 6-4 6 3 6 4-1 1-1 1zm5-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6"/>
          </svg> Profile! </button>
        <div class="m-2" v-if="showProfile"> <MyPro /></div>
      </div>
    </div>
    
  </section>



  <button class="btn btn-outline-dark btn-sm mx-1" @click="toggleList()"> ผลการเรียน </button>
  <button class="btn btn-outline-dark btn-sm mx-1" @click="toggleAdd()"> เพิ่มวิชา </button>
  <div class="m-2" v-if="showStdList"> <SubjList /></div>
  <div class="m-2" v-if="showStdAdd"> <SubjAdd /></div>
</template>

<script>
import MyPro from './components/MyPro.vue';
import SubjAdd from "./components/SubjAdd.vue";
import SubjList from "./components/SubjList.vue";

export default {
  name: "App",
  components: {
    SubjAdd,
    SubjList,
    MyPro,
  },
  data(){
    return{
      showStdAdd: false,
      showStdList: false,
      showProfile: false,
    }
  },
  methods: {
    toggleAdd(){
      this.showStdAdd = !this.showStdAdd;
      this.showStdList = false;
    },
    toggleList() {
      this.showStdList = !this.showStdList;
      this.showStdAdd = false;
    },
    toggleProfile(){
      this.showProfile =! this.showProfile;
      this.showStdAdd = false;
      this.showStdList = false;
    }
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 0px;
  background-image: url('./assets/backG.jpg'); 
  background-size: cover;
  background-position: center; 
}
.img{
box-shadow: -10px -10px 12px 12px rgba(0, 0, 0, 0.37);
border: 10px solid #000000;
}
.btn-lg,  
.display-7,
.display-5,
.display-1{
  text-shadow: -2px -2px 4px rgba(0, 0, 0, 1);
  font-family: "Itim", cursive;
  font-weight: 400;
  font-style: normal;
}
.btn-sm,
.bg-success-subtle{
  font-family: "Itim", cursive;
  font-weight: 400;
  font-style: normal;
}
.mx-1{
   --b: 3px;   /* border thickness */
  --s: .45em; /* size of the corner */
  --color: #373B44;
   padding: calc(.5em + var(--s)) calc(.9em + var(--s));
  color: var(--color);
  --_p: var(--s);
  background:
    conic-gradient(from 90deg at var(--b) var(--b),#0000 90deg,var(--color) 0)
    var(--_p) var(--_p)/calc(100% - var(--b) - 2*var(--_p)) calc(100% - var(--b) - 2*var(--_p));
  transition: .3s linear, color 0s, background-color 0s;
  outline: var(--b) solid #0000;
  outline-offset: .6em;
  font-size: 16px;

  border: 0;

  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}
.mx-1:hover,
.mx-1:focus-visible{
    --_p: 0px;
  outline-color: var(--color);
  outline-offset: .05em;
}
.mx-1:active{
   background: var(--color);
  color: #fff;
}

</style>
