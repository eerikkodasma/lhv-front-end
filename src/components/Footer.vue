<template>
  <div v-if="!isMobile" class="footer">
    <div class="section-wrapper">
      <img src="../assets/images/support.png" alt="headset" />
      <section class="section">
        <h2 class="footer-title">
          LHV <span class="footer-title-bold">Klienditugi</span>
        </h2>
        <p>
          Kui sul tekib pangateenuse kasutamisel probleeme, saad klienditoe
          infotelefonilt abi ööpäev ringi.
        </p>
      </section>
    </div>
    <div class="contact-wrapper">
      <p><img src="../assets/icons/phone.svg" alt="phone" />6 800 400</p>
      <p><img src="../assets/icons/letter.svg" alt="letter" />info@lhv.ee</p>
    </div>
  </div>
  <div v-else class="footer-mobile">
    <div class="footer-mobile-wrapper">
      <img src="../assets/images/support.png" alt="headset" />
      <h2 class="footer-title">
        LHV <span class="footer-title-bold">Klienditugi</span>
      </h2>
      <div class="contact-mobile-wrapper">
        <h2><img src="../assets/icons/phone.svg" alt="phone" />6 800 400</h2>
        <h2>
          <img src="../assets/icons/letter.svg" alt="letter" />info@lhv.ee
        </h2>
      </div>
    </div>
    <p class="footer-mobile-text">
      Kui sul tekib pangateenuse kasutamisel probleeme, saad klienditoe
      infotelefonilt abi ööpäev ringi.
    </p>
  </div>
</template>

<script setup>
import { inject } from "vue";

const isMobile = inject("isMobile");
</script>

<style scoped>
.footer {
  display: flex;
  flex-wrap: wrap;
  padding: 3.75rem 0;
  gap: 1.88rem;
}

.section-wrapper {
  display: flex;
  align-items: center;
  flex: 1;
  gap: 1.5rem;
}

.section {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.footer-title {
  font-weight: 300;
}

.footer-title-bold {
  font-size: 1.38rem;
  line-height: 1.63rem;
  font-weight: 700;
}

.section-wrapper img {
  width: 5rem;
  height: 5rem;
}

.contact-wrapper {
  display: flex;
  align-items: center;
  flex: 1;
  gap: 3rem;
}

.contact-wrapper p {
  display: flex;
  justify-content: right;
  flex: 1;
  gap: 1rem;
  font-weight: 300;
  font-size: 1.38rem;
  line-height: 1.66rem;
}

.contact-wrapper p:last-child {
  text-decoration: underline;
  justify-content: left;
}

.contact-wrapper img {
  width: 1.5rem;
  height: 1.5rem;
  color: #3b3b47;
}

.footer-mobile {
  display: flex;
  flex-direction: column;
  padding: 1.69rem;
  padding-top: 0;
  gap: 3rem;
}

.footer-mobile-text {
  text-align: center;
}

.footer-mobile-wrapper {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  align-items: center;
}

.footer-mobile-wrapper img {
  width: 5rem;
  height: 5rem;
}

.contact-mobile-wrapper {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.contact-mobile-wrapper img {
  width: 1.5rem;
  height: 1.5rem;
  color: #3b3b47;
}

.contact-mobile-wrapper h2 {
  display: flex;
  gap: 1rem;
}
</style>
