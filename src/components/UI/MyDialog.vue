<template>
  <div class="my-modal" v-if="show" @click="hideDialog">
    <div class="modal-dialog" @click.stop>
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title"> {{ title }} </h5>
          <button class="btn-close" @click="hideDialog"></button>
        </div>
        <div class="modal-body">
          <slot></slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "my-dialog",
  props: {
    show: {
      type: Boolean,
      default: false
    },
    title: {
      type: String,
      default: ""
    }
  },
  methods: {
    hideDialog() {
      this.$emit("update:show", false)
    }
  }
}
</script>

<style>
.my-modal {
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.7);
  position: fixed;
  display: flex;
  z-index: 1;
}
</style>