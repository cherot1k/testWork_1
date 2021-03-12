<template>
  <div
      class="about"
      v-touch:swipe.left="transitionLeft"
      v-touch:swipe.top="transitionUp"
      v-touch:swipe.right="transitionRight"
  >
      <aside class="sidebar" >
          <div class="icons ml-3">
            <b-btn class="mx-3 mt-5 icon" variant="light"  @click="$router.push('/')"> <b-img :src="require('../assets/images/icons/Union.svg')"></b-img> </b-btn>
            <b-btn class="mx-3 mt-5 icon" variant="light"  @click="$router.go(0)"> <b-icon-arrow-repeat style="width: 40px; height: 40px; color: #FBA9AF; margin-left: 1px"></b-icon-arrow-repeat> </b-btn>
          </div>
          <div class="content justify-content-end">
            <div class="btn_block">
                <div class="title mx-5">Параметри:</div>
                <div class="row my-5 justify-content-center">
                  <b-row class="choose_btn m-2 col-5">
                    <div class="col" style="padding-left: 0">
                      <b-img class="img_style" :src="require('../assets/images/icons/sad_icon.svg')"></b-img>
                    </div>
                    <span class="col-4 mt-1 selected">{{ chooseFirst }}</span>
                  </b-row>

                  <b-row class="choose_btn m-2 col-5">
                    <div class="col" style="padding-left: 0">
                      <b-img class="img_style"  :src="require('../assets/images/icons/Happy_icon.svg')"></b-img>
                    </div>
                    <span class="col-4 mt-1 selected">{{chooseSecond}}</span>
                  </b-row>

                  <b-row class="choose_btn m-2 col-5" style="background-color: white">
                    <div class="col" style="padding-left: 0">
                      <b-img class="img_style" :src="require('../assets/images/icons/heart_icon.svg')"></b-img>
                    </div>
                    <span class="col-4 mt-1 selected">{{chooseThird}}</span>
                  </b-row>

                </div>
            </div>
          </div>
        <div class="footer row align-items-end">
          <div class="footer_content mr-2 justify-content-center">
             <div class="title">
               <div class="">
                 Осталось в очереди
               </div>
               <div class="d-flex justify-content-center">
                 {{arrayOfMembers.length}}/5
               </div>
             </div>

          </div>
        </div>
      </aside>
      <b-col class="ct col">
        <transition v-for="item in arrayOfMembers" :key="item.name" :name="defaultTransition" >  <!-- name="bounce" -->
          <div class="" :item="currentMember" v-show="data">
            <b-card
                :img-src="require('../assets/images/members/'+ currentMember.photoUrl)"
                img-alt="Image"
                img-top
                img-height="300px"
                tag="article"
                class="mb-2 member_card"
            >
              <b-card-title class="mx-5" style="font-family: Avenir Next Cyr, serif;font-size: 27px;line-height: 39px; color: #8E9AD5; font-weight: bolder; margin-bottom: 7px">
                {{currentMember.name}} <span v-show="false"> {{item.name}} </span>
              </b-card-title>
              <b-card-text class="mx-5" style="font-size: 18px;font-family: Avenir Next Cyr, serif; line-height: 39px;">
                {{currentMember.description}}
              </b-card-text>
              <div class="firstChoosed aid_choosed" v-show="currentMember.selectedBtn==='1st'"> Препарат 1 </div>
              <div class="secondChoosed aid_choosed" v-show="currentMember.selectedBtn==='2nd'"> Препарат 2 </div>
              <div class="thirdChoosed aid_choosed" v-show="currentMember.selectedBtn==='3rd'"> Препарат 3 </div>
            </b-card>
          </div>
        </transition>

        <div class="btn-group">
          <b-btn class="mx-3 submit_btn btn_purple" @click="transitionLeft"> Препарат 1 </b-btn>
          <b-btn class="mx-3 submit_btn btn_blue" @click="transitionUp"> Препарат 2 </b-btn>
          <b-btn class="mx-3 submit_btn btn_yellow" @click="transitionRight"> Препарат 3 </b-btn>
        </div>
      </b-col>
  </div>
</template>

<script>
import {BIconArrowRepeat} from 'bootstrap-vue'
export default {
  components:{
    BIconArrowRepeat
  },
  data(){
    return{
      data: true,
      defaultTransition:'bounce',
      arrayOfMembers:[
        {photoUrl:'member1.png', name:'Lorem ipsum1', description:'lorem loremlorem loremlorem loremlorem loremlorem loremlorem loremlorem lorem', selectedBtn:''},
        {photoUrl:'member2.png', name:'Lorem ipsum2', description:'lorem loremlorem loremlorem loremlorem loremlorem loremlorem loremlorem lorem', selectedBtn:''},
        {photoUrl:'member3.png', name:'Lorem ipsum3', description:'lorem loremlorem loremlorem loremlorem loremlorem loremlorem loremlorem lorem', selectedBtn:''},
        {photoUrl:'member4.png', name:'Lorem ipsum4', description:'lorem loremlorem loremlorem loremlorem loremlorem loremlorem loremlorem lorem', selectedBtn:''},
        {photoUrl:'member5.png', name:'Lorem ipsum5', description:'lorem loremlorem loremlorem loremlorem loremlorem loremlorem loremlorem lorem', selectedBtn:''}
      ],
      chooseFirst:0,
      chooseSecond:0,
      chooseThird:0
    }
  },
  methods:{
    async transitionRight(){
      this.currentMember.selectedBtn='3rd'
      this.defaultTransition = 'bounce'
      this.data = !this.data
      this.chooseThird += 1
      setTimeout(()=>{
        this.deleteMember()
        this.data = !this.data
        this.currentMember.selectedBtn=''
      },600)
    },
    async transitionLeft(){
      this.currentMember.selectedBtn='1st'
      this.defaultTransition = 'debounce'
      this.data = !this.data
      this.chooseFirst += 1
      setTimeout(()=>{
        this.deleteMember()
        this.data = !this.data
        this.currentMember.selectedBtn=''
      },600)
    },
    async transitionUp(){
      this.currentMember.selectedBtn='2nd'
      this.defaultTransition = 'up'
      this.data = !this.data
      this.chooseSecond += 1
      setTimeout(()=>{
        this.deleteMember()
        this.data = !this.data
        this.currentMember.selectedBtn=''
      },600)
    },
    async deleteMember(){
      if(this.arrayOfMembers.length > 1){
        this.arrayOfMembers = this.arrayOfMembers.slice(1)
      }else {
        this.pushToFinal()
      }
    },
    pushToFinal(){
      const first = this.chooseFirst
      const second = this.chooseSecond
      const third = this.chooseThird
      this.$router.push({ path: 'final', query: { first, second, third  } })
    }
  },
  computed:{
    currentMember(){
      return this.arrayOfMembers[0]
    }
  }
}
</script>

<style scoped >
.about{
  display: grid;
  grid-template-columns: repeat(12,1fr);
  grid-template-rows: minmax(0,100vh);
  grid-template-areas:
  "nv nv nv nv ct ct ct ct ct ct ct ct";
  height: 100vh;
  width: 100vw;
  padding: 0;
  margin: 0;
}
.about > .sidebar{
  grid-area: nv;
  background: linear-gradient(63.53deg,
  rgba(45, 133, 80,.83),
  rgba(94, 110, 194,.83));
  display: grid;
  grid-template-columns: 100%;
  grid-template-rows: 1fr 1fr 1fr 1fr;
  grid-template-areas:
      "hd"
      "cn"
      "cn"
      "ft";
  z-index: 5;
  opacity: 1 !important;
}
.about> .ct{
  grid-area: ct;
}

.sidebar > .content{
  /*margin-top: 70%;*/
  grid-area: cn;
  display: grid;
  grid-template-rows: 1fr 1fr 1fr;
  grid-template-columns: 100%;
  grid-template-areas:
    "."
    "end"
    "end";
}
.sidebar > .icons{
  grid-area: hd;
}

.sidebar > .footer{
  grid-area: ft;
}

.content > .btn_block{
  grid-area: end;
}
.title{
  font-family: 'Avenir Next Cyr',serif;
  font-size: 30px;
  line-height: 44px;
  color: white;
}
.choose_btn{
  display: flex;
  justify-items: center;
  border-radius: 40px;
  height: 80px;
  min-width: 100px;
}
.footer_content{
  display: flex;
  flex-direction: row;
  min-height: 100px;
  width: 100%;
  background: rgba(255, 255, 255, 0.15);
  padding: 0;
}

.selected{
  color: #424242;
  font-size: 48px;
  font-weight: bolder;
}

.img_style{
  padding-left: 0;
  height: 80px;
  width: 60px;
  justify-self: start;
}

.icon{
  width: 70px;
  height: 70px;
  border-radius: 50%;
}

.choose_btn{
  background-color: white;
}

.member_card{
  position: absolute;
  top: 20%;
  left: 25%;
  width: 50%;
  height: 530px;
  border-radius: 40px !important;
  z-index: 1;
  overflow: hidden !important;
}

.aid_choosed{
  display: flex;
  justify-content: center;
  align-content: center;
  position: absolute;
  top: 50%;
  left: 10%;
  height: 120px;
  width: 360px;
  font-size: 52px;
  z-index: 10;
}
.thirdChoosed{
  background: linear-gradient(180deg, #FFB903 0%, #FFCA01 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  padding: 0.3em 0.6em ;
  border: 5px solid transparent;
  border-image: linear-gradient(180deg, #FFB903 0%, #FFCA01 100%);
  border-image-slice: 1;
  transform: rotate(15deg);
}
.secondChoosed{
  color: #169AE4;
  border: 5px solid #169AE4;
  transform: rotate(15deg);
}
.firstChoosed{
  color: purple;
  border: 5px solid purple;
  transform: rotate(-15deg);
}
/*for bootstrap photo*/
.card-img-top{
  border-top-left-radius: 40px !important;
  border-top-right-radius: 40px !important;
}
.card-title{
  margin-left: 1em;
  margin-right: 1em;
}
.btn-group{
  position: absolute;
  width: 95%;
  bottom: 10%;
}
.submit_btn{
  height: 80px;
  border-radius: 40px !important;
  color: white;
  font-size: 30px;
}
.btn_purple{
  background: linear-gradient(266.19deg, #8049C7 0%, #CA57FD 100%);
}
.btn_blue{
  background: linear-gradient(266.19deg, #169AE4 0%, #0CC4FA 100%);
}
.btn_yellow{
  background: linear-gradient(90deg, #FFD748 0.02%, rgba(195, 199, 11, 0.96) 99.97%, #CAC6AB 99.98%, #D3E9E1 99.99%);
}

/* animations*/
.bounce-enter-active {
  animation: appear .4s;
}
.bounce-leave-active {
  animation: bounce-in .5s;
}
@keyframes bounce-in {
  0% {
    transform: rotate(0deg) translateX(150px) translateY(230px);
  }
  100% {
    transform: rotate(15deg) translateX(800px) translateY(100px);
  }
}

.debounce-enter-active {
  animation: appear .4s;
}
.debounce-leave-active {
  animation: debounce-in .4s;
}

@keyframes debounce-in {
  0% {
    transform: rotate(0deg) translateX(-150px) translateY(230px);
  }
  100% {
    transform: rotate(-15deg) translateX(-800px) translateY(100px);
  }
}

.up-enter-active {
  animation: appear .4s;
}
.up-leave-active {
  animation: up-in .4s;
}

@keyframes up-in {
  0% {
    transform: rotate(0deg)  translateY(230px);
  }
  100% {
    transform: rotate(-15deg) translateY(-800px);
  }
}

@keyframes appear {
  0% {
    transform: scale(0) translateY(150px);
  }
  50% {
    transform: scale(1.5) translateY(150px);
  }
  100% {
    transform: scale(1) translateY(150px);
  }
}
</style>
