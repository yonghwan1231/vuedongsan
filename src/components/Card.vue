<template>
  <div>
    <img :src="data.image" class="room-img" />
    <h4 @click="send">
      {{ data.title }}
    </h4>
    <p>월 {{ data.price.toLocaleString("ko-KR") }}</p>
  </div>
</template>

<script>
export default {
  name: "CarD",
  props: {
    data: Object,
  },
  methods: {
    send() {
      this.$emit("openModal", this.data.id);
    },
  },
};
</script>

<style>
</style>