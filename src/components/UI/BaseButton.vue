<template>
  <button :type="type" :class="mode">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: ['type', 'mode'],
};
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #967e76;
  border: 1px solid #967e76;
  color: white;
  cursor: pointer;
  border-radius: 10px; /* Add this line to apply rounded edges */
}

button:hover,
button:active {
  background-color: #4f433f;
  border-color: #4f433f;
}

.flat {
  background-color: transparent;
  color: rgba(0, 0, 0, 0.75);
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #d1c5c1;
}
</style>
