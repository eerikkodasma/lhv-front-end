<template>
  <div class="footer">
    <div class="section-wrapper">
      <img src="../assets/images/support.png" alt="headset" />
      <section class="section">
        <h2>LHV <span>Klienditugi</span></h2>
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
</template>

<script setup></script>

<style scoped>
.footer {
  display: flex;
  padding: 3.75rem 0rem;
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

.section h2 {
  font-weight: 300;
}

.section span {
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
</style>
