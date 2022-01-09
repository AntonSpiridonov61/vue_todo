<template>
  <div class="radio_group">
    <label 
      v-for="option in radioOptions" 
      :key="option.value"
      class="form-check-label"
    >
      <input
        class="form-check-input"
        type="radio"
        :value="option"
        v-model="modelValue"
        @change="changeOption"
      />
      {{ option.name }}
    </label>
  </div>
</template>

<script>
export default {
  name: "my-radio",
  props: { 
    modelValue: {
      type: Object
    },
    radioOptions: {
      type: Array,
      required: true
    }
  },
  methods: {
    changeOption(event) {
      this.$emit("update:modelValue", event.target._value)
    }
  }
};
</script>

<style>
.radio_group {
  display: flex;
  flex-direction: column;
  margin-top: 15px;
}
</style>