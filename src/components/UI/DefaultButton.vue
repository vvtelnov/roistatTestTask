<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<script>
  export default {

  }
</script>

<style scoped>
  .button {
    padding: 3px 23px;
    font-size: 18px;
    background-color: rgba(128, 128, 128, 0.222);
    border-radius: 11px;
    border: 1px solid black;
  }

  .button:hover {
    background-color: rgba(0, 128, 128, 0.09);
    border: 1px solid teal;
    color: teal;
  }
</style>