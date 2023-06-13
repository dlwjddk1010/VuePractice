<template>
    <div v-for="(a, i) in onRooms" :key="i">
        <img :src="a.image">
        <!-- <h4 @click="modalOpen = true; click = i"> {{ a.title }}</h4> -->
        <p>{{ a.price }} 만원</p>
    </div>
</template>

<script>
export default {
    name: 'firstCard',
    props: {
        onRooms: Array,
        modalOpen:Boolean,
    }
}
</script>

<style>

</style>