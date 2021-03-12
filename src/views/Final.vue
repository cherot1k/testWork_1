<template>
  <div class="final">
    <img class="right_side_img" :src="require('../assets/images/image.png')">
    <div class="content">
      <div class="icon_block mt-2">
        <div class="col-12">
          <b-btn class="ml-5 mt-5 custom_btn" variant="light" @click="$router.push('/')"> <b-img :src="require('../assets/images/icons/Union_white.png')"></b-img> </b-btn>
        </div>
      </div>
      <div class="result_block" style="color: #424242;">
        <div class="col-10 row ml-auto mb-5 m mt-3">
          <div class="col-4">
            <div class="header">{{aid_1}}%</div>
            <div class="subheader">Препарат 1</div>
          </div>
          <div class="col-4">
            <div class="header">{{aid_2}}%</div>
            <div class="subheader">Препарат 2</div>
          </div>
          <div class="col-4">
            <div class="header">{{aid_3}}%</div>
            <div class="subheader">Препарат 3</div>
          </div>
        </div>
        <div class="col-10 ml-auto">
          <hr/>
        </div>
        <div class="title col-10 ml-auto mt-5">
            <div style="font-weight: 500"> Ваш результат: </div>
            <div style="font-weight: bolder; font-size: 40px;"> «Что я здесь делаю?» </div>
        </div>
        <div class="subtitle col-10 ml-auto mt-3">
          <div class="" style="font-size: 24px; line-height: 29px;color: #424242;"> Это тестовое задание, так что не будем углубляться в глубины проблем фармацевтов.</div>
        </div>


      </div>
      <div class="btn_block">
        <div class="d-flex col-12 mt-5 justify-content-center">
          <b-btn class="again_btn" @click="$router.push('/test')"> Пропробовать ещё </b-btn>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const QUEUE_LEN = 5
export default {
  name: 'Final',
  beforeRouteEnter(to, from, next){
    if(to.query.first && to.query.second && to.query.third){
      next()
    }else {
      next('/')
    }
  },
  mounted() {
    this.calculatePercents(this.$route.query.first, this.$route.query.second, this.$route.query.third)
  },
  data(){
    return{
      aid_1: 0,
      aid_2: 0,
      aid_3: 0
    }
  },
  methods:{
    calculatePercents(first, second , third){
      this.aid_1 = first/QUEUE_LEN * 100
      this.aid_2 = second/QUEUE_LEN * 100
      this.aid_3 = third/QUEUE_LEN * 100
    }
  }
}
</script>

<style scoped>
.final{
  display: grid;
  min-height: 100vh;
  font-family: 'Avenir Next Cyr',serif;
  grid-template-columns: repeat(12,1fr);
  grid-template-rows: auto;
  grid-template-areas:
      "ct ct ct ct ct ct . . . . . .";
}
.final > .content{
  grid-area: ct;
  display: grid;
  grid-template-columns: auto;
  grid-template-rows: 20% 20% 20% 20% 20%;
  grid-template-areas: "ic" "rs" "rs" "." "bt";
}

.content > .icon_block{
  grid-area: ic;
}

.content > .result_block{
  grid-area: rs;
}

.content > .btn_block{
  grid-area: bt;
}

.right_side_img{
  position: absolute;
  right: 0;
  top: 0;
  width: 50%;
  height: 70%;
  border-top-left-radius: 20%;
  border-bottom-left-radius: 30%;
}
.custom_btn{
  width: 70px;
  height: 70px;
  border-radius: 50%;
  color: white;
  background: linear-gradient(63.53deg, #2D8550 16.62%, #5E6EC2 83.38%);
}

.header{
  font-size: 48px;
}

.subheader{
  font-size: 16px;
  font-weight: bolder;
  margin-left: 10px;
}

.title{
  color: #8E9AD5;
  font-size: 36px;
  font-weight: bolder;
  line-height: 35px
}

.again_btn{
  background: linear-gradient(90deg, #D9D9D9 0%, #A1A1A1 100%);
  border-radius: 100px;
  font-size: 24px;
  font-weight: bolder;
  color: white;
  padding: 12px 35px 12px 35px;
}
</style>