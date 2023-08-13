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
  align-self: end;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 2px solid teal;
  cursor: pointer;
}

.btn:hover {
  background: teal;
  color: white;
  transition: 0.3s all;
}
</style>