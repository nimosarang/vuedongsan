<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <h4>{{ oneRooms[누른거].title }}</h4>
      <img :src="oneRooms[누른거].image" class="room-img" />
      <p>{{ oneRooms[누른거].content }}</p>
      <!-- <input @input="month = $event.target.value" /> -->
      <input v-model="month" />
      <p>"{{ month }}개월 선택함 :" {{ oneRooms[누른거].price * month }} 원</p>
      <button @click="closeModal">닫기</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "DetailModal",
  props: {
    oneRooms: Array,
    누른거: Number,
    모달창열렸니: Boolean,
  },
  data() {
    return {
      month: 1,
    };
  },
  watch: {
    month(changedMonth) {
      if (changedMonth > 12) {
        alert("13이상 입력하지 마셈");
        this.month = 1;
      }
      if (isNaN(changedMonth) === true) {
        alert("'개월 수'는 숫자로만 입력해주세요!");
        this.month = 1;
      }
    },
  },
  beforeUpdate() {
    if (this.month == 2) {
      alert("2개월은 너무 적음.. 3개월부터");
      this.month = 3;
    }
  },
  methods: {
    closeModal() {
      this.$emit("bye");
    },
  },
};
</script>
<style></style>
