<template>
  <div
    class="header"
    @mouseover="isCardFlipped = true"
    @mouseleave="isCardFlipped = false"
  >
    <img class="header-image" src="../assets/images/office.png" alt="office" />
    <div
      :class="[
        !isMobile
          ? 'section'
          : !isCardFlipped
          ? 'section-mobile'
          : 'section-mobile-flipped',
      ]"
    >
      <h5 v-if="isMobile && !isCardFlipped">
        Kas sinu diivan on oma aja ära elanud?
      </h5>
      <template v-else>
        <p class="section-text">
          Oled väsinud segadusest, kus asjadel pole oma kohta. Oled unistanud
          lausa täiesti uuest sisekujundusest, aga kõik tundub korraga liiga
          kallis? LHV sisustuslaenuga saad oma unistused ellu viia juba täna.
        </p>
        <BaseButton
          class="header-button"
          :format="FORMATS.TERTIARY"
          @click="scrollToElement"
        >
          Loe lisa
          <template #right-icon>
            <img src="../assets/icons/down-arrow.svg" alt="arrow" />
          </template>
        </BaseButton>
      </template>
    </div>
    <img
      v-if="isMobile"
      :class="['mobile-image', isCardFlipped && 'mobile-image-hidden']"
      src="../assets/images/corner-white-bg.png"
      alt="corner-white"
    />
  </div>
</template>

<script setup>
import BaseButton from "@/components/base_components/BaseButton.vue";
import { FORMATS } from "@/enums/components";
import { ref, inject } from "vue";

const isMobile = inject("isMobile");
const isCardFlipped = ref(false);

function scrollToElement() {
  const element = document.getElementById("calculator");
  if (element) {
    element.scrollIntoView({ behavior: "smooth" });
  }
}
</script>

<style scoped>
.header {
  display: flex;
  position: relative;
  background-color: #8ecdd1;
  padding: 3.75rem 2.5rem 3.75rem 18.38rem;
  margin: 0 0 3.94rem 5.06rem;
  border-radius: 0.25rem;

  @media screen and (max-width: 600px) {
    margin: 0 2.5rem;
    padding: 0;
    cursor: pointer;
  }
}

.header-image {
  position: absolute;
  width: 18.38rem;
  height: 18.38rem;
  top: 57px;
  left: -5.06rem;
  border-radius: 0.25rem;

  @media screen and (max-width: 600px) {
    position: static;
    width: 100%;
  }
}

.section {
  display: flex;
  flex-direction: column;
  gap: 0.81rem;
}

.section-mobile {
  position: absolute;
  height: 6.63rem;
  background-color: #8ecdd1;
  width: 100%;
  bottom: 0;
  padding: 1.25rem 3.19rem 1.25rem 1.5rem;
}

.section-mobile-flipped {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  position: absolute;
  height: 100%;
  width: 100%;
  background-color: #8ecdd1;
  padding: 1.5rem;
}

.section-text {
  padding-right: 2.56rem;
}

h5 {
  font-weight: 700;
}

.header-button {
  font-weight: 700;
  padding: 0;
}

.mobile-image {
  width: 3.19rem;
  height: 3.19rem;
  position: absolute;
  right: 0;
  bottom: 0;
}

.mobile-image-hidden {
  display: none;
}
</style>
