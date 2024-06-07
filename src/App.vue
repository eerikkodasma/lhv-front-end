<template>
  <div class="main">
    <Header />
    <Calculator />
    <Footer />
  </div>
</template>

<script setup>
import Calculator from "@/components/Calculator.vue";
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
</script>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  max-width: 58.88rem;
  gap: 3.75rem;
}
</style>
