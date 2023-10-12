<template>
<button
  class="nesting-control-button"
  :class="classAppearingModificator"
>></button>
</template>

<script>
export default {
  props: {
    classAppearingModificator: {
      type: String,
      required: true,
    }
  },
}
</script>

<style scoped>
.nesting-control-button {
  background-color: rgb(255, 255, 255);
  border: none;
  font-size: 14px;
  line-height: 1.3;
  font-weight: 400;
}

.nesting-control-button:hover {
  color: rgb(0, 128, 128);
  font-weight: 600;
}
 
.nesting-control-button_action_expand {
  transform: rotate(90deg);
}

.nesting-control-button_action_hide {
  transform: rotate(0deg);
}

.nesting-control-button_visibility_hidden {
  visibility: hidden;
}
</style>