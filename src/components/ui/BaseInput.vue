<template>
  <div class="d-flex field">
    <slot name="beforeInput"></slot>
    <input
      type="text"
      class="form-control"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      @change="$emit('onChange', $event.target.value)"
    />
    <slot name="afterInput"></slot>

  </div>
</template>

<script>
export default {
  name: "BaseInput",
  props: {
    modelValue: {
      type: [String, Number],
      default: ''
    },
  }
};

</script>

<style>
.field{
  background: whitesmoke;
  padding: 0;
  border: 0;
}
</style>