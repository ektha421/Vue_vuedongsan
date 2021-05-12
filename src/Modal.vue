<template>
  <div class="black-bg" v-if="isOpen">
    <div class="white-bg">
      <h4>{{products[press].title}}</h4>      
      <P>{{products[press].content}}</P>
       <input v-model.number="month" placeholder="개월 수를 입력해주세요"/>
      <P>{{month}}개월 선택함 : {{products[press].price*month}}원</P>
      <button class="btn-close" @click="$emit('closeModal')">닫기</button> 
    </div>
  </div>
</template>

<script>
export default {
    name: 'Modal',
    props:{
      products: Object,
      press: Number,
      isOpen: Boolean
    },
     data() {
        return{
          month: 1,
        }
    },
    watch:{
      month(a){
        if(isNaN(a)){
          alert('숫자만 입력해주세요');
          this.month = 1;
        }
      }
    },
      beforeUpdate(){
        if(this.month == 2){
          alert('2개월 노노');
          this.month = '3'
        }
  },
}
</script>

<style>

</style>