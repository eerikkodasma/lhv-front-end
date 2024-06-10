<template>
  <div class="modal-overlay">
    <div class="modal-wrapper">
      <div :class="['modal-header', !title && 'modal-header-no-title']">
        <div v-if="title" class="modal-title">{{ title }}</div>
        <button class="close-button" @click="$emit('close')">×</button>
      </div>
      <div class="modal-content">
        <slot name="content"></slot>
      </div>
      <div>
        <slot name="footer"></slot>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  title: {
    type: String,
    required: false,
  },
});
</script>

<style scoped>
.modal-overlay {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  inset: 0;
  z-index: 9999;
}

.modal-wrapper {
  display: flex;
  flex-direction: column;
  background: white;
  border-radius: 1.88rem;
  max-width: 90%;
  padding: 2.5rem;
  width: 25rem;
  gap: 1.5rem;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  gap: 0.5rem;
}

.modal-header-no-title {
  justify-content: flex-end;
}

.modal-title {
  font-size: 1.25rem;
  font-weight: 500;
  line-height: 1.75rem;
}

.close-button {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}
</style>
