<template>

<first-modal :onRooms="onRooms" :click="click" :modalOpen="modalOpen" />


<!-- <div v-if="modalOpen" class="black-bg">
  <div class ="white-bg">
    <img :src="onRooms[click].image" style = "width:100%;"> 
    <h4>{{onRooms[click].title}}</h4>
    <p>{{ onRooms[click].price}}</p>
    <button @click="modalOpen=false">닫기</button>
  </div>
</div>
<first-modal /> -->


  <div class = "menu">
    <!-- <a v-for="a in menus" :key="a">{{ a }}</a> -->
    <!-- a가 menus의 각 값이 됨 -->
    <a v-for="(a, i) in menus" :key="i">{{ a }}</a>
    <!-- (a, i) ==>> a : 각 요소의 값, i : 각 요소의 index 번호 -->
  </div>

  <!-- <div v-for="(a, i) in 3" :key="i">
    <h4 class="red" :style="style" >{{ products[i] }}</h4>
    <p>{{ price1 }} 만원</p>
  </div> -->
  <!-- <div v-for="(a, i) in products" :key="i">
    <h4 class="red" :style="style" >{{ a }}</h4>
    <p>{{ price1 }} 만원</p>
  </div> -->


  <!-- <div>
    <img src="./assets/logo.png">
    <h4> {{products[0]}}</h4>
    <p>{{ price2 }} 만원</p>
    <button @click="reportCntPlus">허위 매물 신고</button>
    <span>신고 수 : {{ reportCnt }}</span>
  </div>
  <div>
    <img src="./assets/logo2.png">
    <h4> {{products[1]}}</h4>
    <p>{{ price2 }} 만원</p>
  </div>
  <div>
    <img src="./assets/logo3.png">
    <h4> {{products[2]}}</h4>
    <p>{{ price2 }} 만원</p>
  </div> -->

  <!-- <div v-for="(a, i) in products" :key="i">
      <h4> {{ a }}</h4>
      <p>{{ price2 }} 만원</p>
      <button @click="reportCntPlus(i)">허위 매물 신고</button>
      <span>신고 수 : {{ reportCnts[i] }}</span>
    </div> -->

    <first-compo />
    <first-card :onRooms="onRooms" :modalOpen="modalOpen"/>

    <div v-for="(a, i) in onRooms" :key="i">
      <img :src="a.image">
      <h4 @click="modalOpen=true; click= i"> {{ a.title }}</h4>
      <p>{{ a.price }} 만원</p>
    </div>
    
</template>

<script>
import data from './data.js';
import firstCompo from './firstCompo.vue'
import firstModal from './firstModal.vue'
import firstCard from './firstCard.vue'

export default {
  name: 'App',
  data() {  //데이터 보관함...? react에서는 state라고 부름
    return {
      price1: 50,
      price2: 70,
      style: 'color:blue',
      products: ['역삼동 원룸', '천호동 원룸', '마포구 원룸'],
      menus: ['Home', 'Shop', 'About'],
      reportCnt: 0,
      reportCnts: [0, 3, 0],
      modalOpen: false,
      onRooms: data,
      click: 0,
      object:{name:"dd", age:20}
    }
  },
  methods: { // 함수 만드는 공간
    reportCntPlus(i) {
      this.reportCnts[i]++
    }
  },
  components: {
    firstCompo,
    firstModal,
    firstCard,
  }
}
</script>

<style>
.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
body{
  margin:0
}
div{
  box-sizing: border-box;
}
.black-bg{
  width:100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}
.white-bg{
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

</style>

<!-- 
문법 쓰는 이유
1. 하드코딩 해놓으면 변경이 어려움 그래서 {{데이터 바인딩 하는 거임}}
2. 실시간 자동 렌더링을 쓰기 위해서 -> 데이터를 변경하면 변경사항이 {{알아서 반영이 됨}}

자주 변경되지 않는 데이터는 바인딩 할 필요가 없음 (ex 로고, 치수 그런 거)
==> 자주 변경되는 데이터들은 바인딩 되도록 보관

태그 외부를 바인딩하고 싶으면 {{}}
태그 내부의 속성을 바인딩 하고 싶으면 :style="" 이런 식으로 사용 가능

v-for="" vue 반복문
- v-for="작명 in 반복수/데이터" :key
- :key 안 하면 에러 남
-> :key의 용도 == 반복문이 돌면서 변하는 유니크한 숫자 / 반복문 돌린 요소를 컴퓨터가 구분하기 위해 씀

v-on:click == @click
@mouseover : 마우스 갖다 댔을 때 
@input : 입력했을 때
.
.

v-if="조건식"
- 참일 때만 보여줌
v-else
- 위에 거가 참이 아닐 때 보여줌
v-else-if="조건식"
- if 아닐 때 검사해봄

methods 위치 -> data 밑
함수 내부에서 데이터를 가져다 쓰기 위해서는 this.을 붙여야 함

동적인 UI 만드는 방법
1. UI의 현재 상태를 데이터로 저장
2. 데이터에 따라 UI가 어떻게 보일지 작성

한 개 export = export default apple - import apple from ~
여러 개 export = export {apple1, apple2} - immport {apple1, apple2} from ~

축약 해놓은 component 사용하는 방법
1. vue 파일 import
2. 등록
3. 사용

component를 사용하는 이유
- 가독성
- 반복적으로 사용할 가능성이 있기 때문 (재사용이 쉬움)

데이터 파인딩은 밑에 데이터가 있어야 가능함

props
- 자식 컴포넌트가 부모가 갖고 있는 데이터를 쓰려면 porps로 데이터를 전송해야 함
- read-only라서 받아온 거 수정하면 안 됨
1. 데이터를 정송
2. 등록
3. 사용
보낼 때 : <사용할vue :보낼데이터이름="보낼데이터" />
  - 작명="문자자료" / :작명="숫자자료"
사용할 때
props:{
   이름 : 타입(Array, Number...)
}

-->