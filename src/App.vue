<template>
  <div class="menu">
    <a v-for="a in menus" :key="a">{{ a }}</a>
  </div>

  <div class="start" :class="{ end: 모달창열렸니 }">
    <DetailModal
      :oneRooms="oneRooms"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
      @bye="모달창열렸니 = false"
    />
  </div>

  <DiscountInfo :count="count" v-if="showDiscount == true" />

  <button @click="sortPrice">가격순 정렬</button>
  <button @click="sortBack">원래대로</button>
  <button @click="filter50man">50만원 이상만 보기</button>

  <MainCard
    @openModal="
      모달창열렸니 = true;
      누른거 = $event;
    "
    :oneRoom="oneRooms[i]"
    v-for="(oneRoom, i) in oneRooms"
    :key="i"
  />
</template>

<script>
import data from "./assets/oneroom.js";
import DiscountInfo from "./Discount.vue";
import DetailModal from "./DetailModal.vue";
import MainCard from "./Card.vue";

export default {
  name: "App",
  data() {
    return {
      count: 5,
      showDiscount: true,
      누른거: 0,
      oneRoomsOriginal: [...data],
      oneRooms: [...data],
      모달창열렸니: false,
      신고수: Array(data.length).fill(0),
      menus: ["Home", "Shop", "About"],
    };
  },
  methods: {
    sortBack() {
      this.oneRooms = [...this.oneRoomsOriginal];
    },
    sortPrice() {
      this.oneRooms.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    filter50man() {
      this.oneRooms = this.oneRoomsOriginal
        .filter((a) => a.price >= 500000)
        .sort((a, b) => a.price - b.price);
    },
  },
  mounted() {
    let interval = setInterval(() => {
      this.count--;
      if (this.count == 0) {
        clearInterval(interval);
        this.showDiscount = false;
      }
    }, 1000);
  },
  components: {
    DiscountInfo,
    DetailModal,
    MainCard,
  },
};
</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}

.start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
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
