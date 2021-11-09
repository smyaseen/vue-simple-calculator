<template>
  <button @click="$emit('onClick')" class="btn">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
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
