<template>
  <div class="main">
    <h1 class="title" v-if="isMobile">Sisustuslaen</h1>
    <Header />
    <Calculator />
    <Footer />
  </div>
</template>

<script setup>
import Calculator from "@/components/Calculator.vue";
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import { ref, provide } from "vue";

const isMobile = ref(window.innerWidth <= 600);
provide("isMobile", isMobile);

window.addEventListener("resize", () => {
  isMobile.value = window.innerWidth <= 600;
});
</script>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  max-width: 58.88rem;
  gap: 3.75rem;

  @media screen and (max-width: 600px) {
    gap: 3rem;
  }
}

.title {
  margin: 2.5rem auto 0;
}
</style>
