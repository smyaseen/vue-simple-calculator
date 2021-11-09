<template>
  <button @click="$emit('onClick')" class="btn" :disabled="disableButtons">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    disableButtons: Boolean,
  },
  emits: ["onClick"],
};
</script>

<style scoped>
.btn {
  margin-top: 10px;
  margin-right: 2px;
  height: 50px;
  width: 140px;
}
</style>
