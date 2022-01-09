<template>
  <select 
    class="form-select form-select-sm"
    style="width: 200px"
    v-model="modelValue" 
    @change="changeOption">
    <option disabled value="">Выберете из списка</option>
    <option 
      v-for="option in options"  
      :key="option.value"
      :value="option.value"
    >
      {{ option.name }}
    </option>
  </select>
</template>

<script>
export default {
  name: "my-select",
  props: {
    modelValue: {
      type: String
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event) {
      this.$emit("update:modelValue", event.target.value)
    }
  }
}
</script>

<style>

</style>