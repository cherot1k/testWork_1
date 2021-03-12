<template>
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
</template>

<script>
export default {
  props:{
    currentMember:{
      type: Object,
      required: true
    },
    item:{
      type: Object,
      required: true
    }
  }
}
</script>