<template>
  <div v-if="modalOpen" class="black-bg">
      <div class ="white-bg">
        <img :src="onRooms[click].image" style = "width:100%;"> 
        <h4>{{ onRooms[click].title }}</h4>
        <p>{{ onRooms[click].price }}</p>
        <!-- <button @click="modalOpen = false">닫기</button> -->
      </div>
    </div>
</template>

<script>
export default {
  name :'firstModal',
  props: {
    onRooms:Array,
    click: Number,
    modalOpen:Boolean
  }
}
</script>

<style>

</style>