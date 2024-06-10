<template>
  <div class="input-container">
    <div class="input-wrapper">
      <slot name="iconBefore"></slot>
      <input
        class="input"
        :value="modelValue"
        :id="id"
        :type="type === 'number' && acceptsCommas ? 'text' : type"
        :name="name"
        :placeholder="placeholder"
        @input="handleInput($event.target.value)"
      />
      <slot name="iconAfter"></slot>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  modelValue: {
    type: [String, Number, Boolean, null],
    default: undefined,
  },
  id: {
    type: String,
    required: true,
  },
  name: {
    type: String,
    required: true,
  },
  placeholder: {
    type: String,
    default: undefined,
  },
  required: {
    type: Boolean,
    default: false,
  },
  type: {
    type: String,
    default: "text",
  },
  acceptsCommas: {
    type: Boolean,
    default: false,
  },
});

function handleInput(value) {
  if (props.type === "number") {
    if (props.acceptsCommas) {
      value = value.replace(",", ".");

      // Count the number of dots and allow only one dot
      const dotCount = (value.match(/\./g) || []).length;
      if (dotCount > 1) {
        value = props.modelValue;
      }

      // Replace all non-numbers
      value = value.replace(/[^0-9,.]/g, "");

      // Only allow 2 decimal points
      let match = value.match(/^(\d+)(\.\d{0,2})?/);
      value = match ? match[0] : "";
    }
  }
  emit("update:modelValue", value);
}

const emit = defineEmits(["update:modelValue"]);
</script>

<style scoped>
.input-container {
  display: flex;
  flex-direction: column;
}

.input-wrapper {
  display: flex;
}

.input {
  width: 100%;
}
</style>
