<template lang="kor">
  <div>
    <img :src="oneRoom.image" class="room-img" />
    <h4 @click="openModal">{{ oneRoom.title }}</h4>
    <p>{{ oneRoom.price }}원</p>
  </div>
</template>

<script>
export default {
  name: "MainCard",
  props: {
    oneRoom: Object,
  },
  methods: {
    openModal() {
      this.$emit("openModal", this.oneRoom.id);
    },
  },
};
</script>
<style lang="kor"></style>
