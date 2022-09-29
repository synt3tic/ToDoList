<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "my-button",
};
</script>

<style scoped>
.btn {
  height: 40px;
  background: none;
  color: teal;
  border: 2px solid teal;
  border-radius: 10px;
}

.btn:hover {
  cursor: pointer;
  background: teal;
  color: white;
}
</style>