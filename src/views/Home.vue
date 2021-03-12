<template>
  <div class="home">
    <div class="some">
      <b-container class="bv-example-row">
        <div class="abs align-content-center">
          <b-row class="h-100 w-100 justify-content-center content" style="position: absolute" align-v="center">
            <b-col cols="2"></b-col>
            <b-col cols="8" class="mt-5">
              <b-row class="col-12 ml-3 mb-3"> <h1 class="title_1"> Добро пожаловать в игру </h1> </b-row>
              <b-row class="col-12 mb-5 justify-content-center ">
                <b-row  class="title_2 col-12 white"> <div class="col-12">Помоги</div> </b-row>
                <b-row  class="title_2 col-12 white"> <div class="col-12">ФАРМАЦЕВТУ</div>  </b-row>
              </b-row>
              <b-row class="go_btn justify-content-center"> <b-button class="btn_itself" href="#" variant="light" @click="$router.push('/test')">Начать</b-button> </b-row>
            </b-col>
            <b-col cols="2"></b-col>
          </b-row>
        </div>
      </b-container>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',

}
</script>

<style scoped>
.home{
  display: flex;
  min-height: 100vh;
  font-family: 'Avenir Next Cyr',serif;
}
.some{
  height: 100vh;
  width: 100vw;
  background: linear-gradient(63.53deg,
      rgba(45, 133, 80,.5),
      rgba(94, 110, 194,.5)),
  url('~@/assets/images/mainPageBackGround.png');
}

.abs{
  display: flex;
  position: absolute;
  top:0;
  left:7%;
  min-width: 800px;
  min-height: 800px;
  /*background-image: url("~@/assets/images/mainPageEllipse.png") !important;*/
  z-index: 3;
  border-radius: 50%;
  background: linear-gradient(63.53deg, #2D8550 16.62%, #5E6EC2 83.38%);
  opacity: 1;
}
.title_1{
  color:white;
  font-size: 35px;
  line-height: 41px;
  letter-spacing: 0.02em
}
.title_2{
  font-size: 60px;
  font-weight: bold;
  line-height: 66px;
  display: flex;
  align-items: center;
  letter-spacing: 0.02em;
}
.go_btn{
  margin-top: 120px !important;

}
.btn_itself{
  padding: 10px 100px 10px 100px !important;
  border-radius: 40px !important;
  font-size: 35px !important;
  color:gray !important;
}
.white{
  color: white;
}
</style>