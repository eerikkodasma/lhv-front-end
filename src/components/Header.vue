<template>
  <div class="header">
    <img class="header-image" src="../assets/images/office.png" alt="office" />
    <div class="section">
      <h5>Kas sinu diivan on oma aja ära elanud?</h5>
      <p class="section-text">
        Oled väsinud segadusest, kus asjadel pole oma kohta. Oled unistanud
        lausa täiesti uuest sisekujundusest, aga kõik tundub korraga liiga
        kallis? LHV sisustuslaenuga saad oma unistused ellu viia juba täna.
      </p>
      <BaseButton class="header-button" :format="FORMATS.TERTIARY">
        Loe lisa
        <template #right-icon>
          <img src="../assets/icons/down-arrow.svg" alt="arrow" />
        </template>
      </BaseButton>
    </div>
  </div>
</template>

<script setup>
import BaseButton from "@/components/base_components/BaseButton.vue";
import { FORMATS } from "@/enums/components";
</script>

<style scoped>
.header {
  position: relative;
  background-color: #8ecdd1;
  padding: 3.75rem 2.5rem 3.75rem 18.38rem;
  margin: 0 0 3.94rem 5.06rem;
  border-radius: 0.25rem;
}

.header-image {
  position: absolute;
  width: 18.38rem;
  height: 18.38rem;
  top: 57px;
  left: -5.06rem;
  border-radius: 0.25rem;
}

.section {
  display: flex;
  flex-direction: column;
  gap: 0.81rem;
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
</style>
