<template>
  <div class="discount">
    <h4>지금 결제하면 {{ count }}% 할인!!</h4>
  </div>
</template>

<script>
export default {
  name: "DiscountInfo",
  props: { count: Number },
  data() {
    return {};
  },
  methods: {
    counting() {
      setInterval(() => {
        this.disNum--;
      }, 1000);
    },
  },
};
</script>

<style></style>
