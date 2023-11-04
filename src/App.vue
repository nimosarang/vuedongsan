<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <h4>{{ oneRooms[누른거].title }}</h4>
      <img :src="oneRooms[누른거].image" class="room-img" />
      <p>{{ oneRooms[누른거].content }}</p>
      <button @click="모달창열렸니 = false">닫기</button>
    </div>
  </div>

  <div class="menu">
    <a v-for="a in menus" :key="a">{{ a }}</a>
  </div>

  <div
    v-for="({ title, image, price }, index) in oneRooms"
    :key="oneRooms[index].id"
  >
    <img :src="image" class="room-img" />
    <h4
      @click="
        모달창열렸니 = true;
        누른거 = index;
      "
    >
      {{ title }}
    </h4>
    <p>{{ price }}원</p>
    <button @click="increase(index)">허위매물 신고</button>
    <span>신고수 : {{ 신고수[index] }}</span>
  </div>
</template>

<script>
import data from "./assets/oneroom.js";

export default {
  name: "App",
  data() {
    return {
      누른거: 0,
      oneRooms: data,
      모달창열렸니: false,
      신고수: Array(data.length).fill(0),
      menus: ["Home", "Shop", "About"],
    };
  },
  methods: {
    increase(index) {
      this.신고수[index]++;
    },
  },
  components: {},
};
</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img {
  width: 50%;
  margin-top: 40px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
</style>
