<template>
  <transition name="fade">
    <Modal
      :원룸들="원룸들"
      :클릭한원룸="클릭한원룸"
      :모달창표시="모달창표시"
      @closeModal="this.모달창표시 = false"
    />
  </transition>

  <div class="menu">
    <a v-for="(el, idx) in 메뉴들" :key="idx">{{ el }}</a>
  </div>
  <Discount v-if="showDiscount == true" />

  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card
    v-for="(el, idx) in 원룸들"
    :key="idx"
    :data="el"
    @openModal="
      this.모달창표시 = true;
      this.클릭한원룸 = $event;
    "
  />
</template>

<script>
import oneroom from "./assets/oneroom";
import Discount from "./components/Discount.vue";
import Modal from "./components/Modal.vue";
import Card from "./components/Card.vue";

export default {
  name: "App",
  data() {
    return {
      모달창표시: false,
      클릭한원룸: 0,
      메뉴들: ["Home", "Product", "About"],
      원룸들: [...oneroom],
      신고수: [0, 0, 0],
      showDiscount: true,
    };
  },
  methods: {
    increase() {
      this.신고수[0] += 1;
    },
    modalClose() {
      this.모달창표시 = !this.모달창표시;
    },
    modalOpen(idx) {
      this.모달창표시 = true;
      this.클릭한원룸 = idx;
    },
    priceSort() {
      this.원룸들.sort((a, b) => {
        return a.price - b.price;
      });
    },
    sortBack() {
      this.원룸들 = [...oneroom];
    },
  },
  components: {
    Discount,
    Modal,
    Card,
  },

  mounted() {
    setTimeout(() => {
      this.showDiscount = false;
    }, 2000);
  },
};
</script>

<style>
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

#app {
  text-align: center;
}

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
  width: 100%;
  margin-top: 40px;
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
