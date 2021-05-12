<template>
  <div class="menu">
    <a v-for="(item, index) in menu" :key="index">{{item}}</a>
  </div>

  <transition name="fade">
    <Modal 
    :products="products" 
    :isOpen="isOpen" 
    :press="press"
    @closeModal = "isOpen = false"
    />
  </transition>

  <Discount :discountPercent="discountPercent"/>

  <button @click="priceSort">가격낮은순정렬</button>
  <button @click="priceHightSort">가격높은순정렬</button>
  <button @click="stringSort">가나다순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card
  @openModal = "isOpen = true; press = $event" 
  :products="products[index]" 
  :count1="count1" v-for="(product, index) in products" :key="index"/>

</template>

<script>
import data from './assets/oneroom';
import Discount from './Discount';
import Modal from './Modal';
import Card from './Card';

export default {
  name: "App",
  components: { Discount, Modal, Card },
  data() {
    return {
      showDiscount: true,
      discountPercent: 5,
      press: 0,
      isOpen: false,
      count1: 0,
      count2: 0,
      count3: 0,
      originProducts: [...data],
      products: data,
      menu: ["Home","Shop","About"]
    };
  },
  mounted(){
    // setTimeout(() => {    
    //   this.showDiscount = false;
    // },2000);

     setInterval(() => {    
      this.discountPercent -= 1;
    },1000);
  },
  unmounted(){
    // if(this.discountPercent === 0){
    //   setInterval.destroy()
    // }
  },
   methods: {
    increaseClick(num){
      if(num === 1){
      this.count1 += 1
      } else if(num === 2){
         this.count2 += 1
      } else if(num === 3){
         this.count3 += 1
      }
    },
    sortBack(){
      this.products = [...this.originProducts];
    },
    priceSort(){
      this.products.sort(function(a,b){
        return a.price - b.price 
      })
    },
    priceHightSort(){
      this.products.sort(function(a,b){
        return b.price - a.price 
      })
    },
    stringSort(){
      this.products.sort(function(a,b){
        if(a.title < b.title){
          return -1;
        }else if(a.title == b.title){
          return 0;
        }else{
          return 1;
        } 
      })
    }
  },

};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}
.menu{
  background: skyblue;
  padding:15px;
  border-radius:5px;
}
.menu a{
  color: #fff;
  padding: 10px;
}
.discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.room-img{
  width:100%;
  margin-top:40px;
}
body{
  margin: 0;
}
div{
  box-sizing: border-box;
}
.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed;
  padding: 20px;
}
.white-bg{
  width: 100%;
  background: #fff;
  border-radius: 8px;
  padding: 20px;
}
.start{
  opacity: 0;
  transition: all 1s;
}
.end{
  opacity: 1;
}
.fade-enter-from{
  opacity: 0;
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  opacity: 1;
}
.fade-leave-from{
  opacity: 1;
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
  opacity: 0;
}
</style>
