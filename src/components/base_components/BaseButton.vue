<template>
  <button
    v-bind="$attrs"
    :class="{ btn: true, [`btn--${format}`]: format }"
    :type="type"
    :disabled="disabled"
    @click="onClick"
  >
    <slot name="left-icon"></slot>
    <slot>Click me!</slot>
    <slot name="right-icon"></slot>
  </button>
</template>

<script setup>
import { FORMATS } from "@/enums/components";
const props = defineProps({
  type: {
    type: String,
    default: "button",
  },
  disabled: {
    type: Boolean,
    default: false,
  },
  format: {
    type: String,
    default: FORMATS.PRIMARY,
  },
});

const onClick = (event) => {
  if (props.disabled) {
    event.preventDefault();
    return;
  }
  emits("onClick", event);
};

const emits = defineEmits(["onClick"]);
</script>

<style>
.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: fit-content;
  cursor: pointer;
  border: none;
  gap: 0.5rem;
  font-size: 0.88rem;
  line-height: 1.25rem;
  font-weight: 400;
  padding: 0.5rem 1rem;
  border-radius: 0.25rem;
}

.btn--primary {
  background-color: #3b3b47;
  color: #ffffff;
}

.btn--tertiary {
  background: none;
}
</style>
