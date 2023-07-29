<template>
  <div class="black-bg" v-if="모달창표시">
    <div class="white-bg">
      <img :src="원룸들[클릭한원룸].image" class="room-img" />
      <h4>{{ 원룸들[클릭한원룸].title }}</h4>
      <p>{{ 원룸들[클릭한원룸].content }}</p>
      <input type="text" v-model="month" />
      <select v-model="month">
        <option>12</option>
        <option>24</option>
      </select>

      <p>월 {{ 원룸들[클릭한원룸].price * month }}</p>
      <p>{{ month }}개월 선택함</p>
      <Discount />
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MoDal",
  data() {
    return {
      month: 1,
    };
  },
  watch: {
    month() {
      if (isNaN(this.month)) {
        alert("숫자만 입력해라");
        this.month = 1;
      }
      if (this.month > 13) alert("12개월 이하로 입력해라.");
    },
    date() {},
  },
  props: {
    원룸들: Array,
    클릭한원룸: Number,
    모달창표시: Boolean,
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
</style>