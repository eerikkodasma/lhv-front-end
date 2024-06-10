<template>
  <ModalWrapper
    :title="!loanSuccess ? 'Isiklikud detailid' : undefined"
    @close="$emit('close')"
  >
    <template v-if="!loanSuccess" #content>
      <form id="userDetailsForm" class="form" @submit.prevent="submitForm">
        <BaseInput
          v-model="form.firstName"
          id="firstName"
          name="firstName"
          label="Eesnimi"
          placeholder="Eesnimi"
          required
          :errors="errors['firstName']"
        />
        <BaseInput
          v-model="form.lastName"
          id="lastName"
          name="lastName"
          label="Perekonnanimi"
          placeholder="Perekonnanimi"
          required
          :errors="errors['lastName']"
        />
        <BaseInput
          v-model="form.mobileNumber"
          id="mobileNumber"
          name="mobileNumber"
          label="Mobiilinumber"
          placeholder="Mobiilinumber"
          type="number"
          required
          :errors="errors['mobileNumber']"
        />
        <BaseInput
          v-model="form.email"
          id="email"
          name="email"
          label="E-post"
          placeholder="E-post"
          type="email"
          required
          :errors="errors['email']"
        />
      </form>
    </template>
    <template v-else #content>
      <h1 class="loan-success-text">Sisustuslaen edukalt taoteldud!</h1>
    </template>
    <template v-if="!loanSuccess" #footer>
      <BaseButton
        form="userDetailsForm"
        type="submit"
        @click.prevent.stop="submitForm()"
        >Taotle</BaseButton
      >
    </template>
  </ModalWrapper>
</template>

<script setup>
import BaseButton from "@/components/base_components/BaseButton.vue";
import BaseInput from "@/components/base_components/BaseInput.vue";
import ModalWrapper from "@/components/ModalWrapper.vue";
import { ref } from "vue";
const emits = defineEmits(["close"]);
const errors = ref({});
const loanSuccess = ref(false);

const form = ref({
  firstName: "",
  lastName: "",
  mobileNumber: "",
  email: "",
});

const submitForm = () => {
  // Reset errors before validating
  errors.value = {};
  const result = validateForm(form.value);
  if (result) loanSuccess.value = true;
};

const validateForm = (form) => {
  if (!form.firstName) {
    errors.value["firstName"] = ["Eesnimi on kohustuslik"];
  }
  if (!form.lastName) {
    errors.value["lastName"] = ["Perekonnanimi on kohustuslik"];
  }
  if (!form.mobileNumber) {
    errors.value["mobileNumber"] = ["Mobiilinumber on kohustuslik"];
  } else {
    if (!/^5\d{6,7}$/.test(form.mobileNumber)) {
      errors.value["mobileNumber"] = [
        "Mobiilinumber peab olema 7- või 8-kohaline ja algama 5-ga",
      ];
    }
  }
  if (!form.email) {
    errors.value["email"] = ["E-post on kohustuslik"];
  } else {
    if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
      errors.value["email"] = ["E-post peab olema korrektses vormis"];
    }
  }

  return Object.keys(errors.value).length === 0;
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.loan-success-text {
  text-align: center;
}
</style>
