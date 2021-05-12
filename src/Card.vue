<template>
  <div>
    <img :src="products.image" class="room-img">
    <h4 @click="$emit('openModal',products.id)">{{products.title}}</h4>
    <P>{{products.price}}만원</P>
    <button type="button" @click="increaseClick(1);press=index">허위매물신고</button>
    <span>신고수: {{count1}}</span>
  </div>
</template>

<script>
export default {
    props:{ 
        products: Object, 
        count1: Number, 
        isOpen: Boolean 
    },
   

}
</script>

<style>

</style>