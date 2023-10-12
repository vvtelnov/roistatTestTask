<template>
<button
  class="nesting-control-button"
  :class="classAppearingModificator"
  @click="$emit('nestingControlButtonClicked')"
>></button>
</template>

<script>
export default {
  props: {
    classAppearingModificator: {
      type: String,
      required: true,
      default: '',
    }
  },
  methods: {
    // expandBtnClickHandler(evt) {
      
    // }
  }
}
</script>

<style scoped>
.nesting-control-button {
  background-color: rgb(255, 255, 255);
  border: none;
  font-size: 14px;
  line-height: 1.3;
  font-weight: 400;
  transform: rotate(90deg);
}

.nesting-control-button:hover {
  color: rgb(0, 128, 128);
  font-weight: 600;
}
 
.nesting-control-button_action_expand {
  transform: rotate(0deg);
}

.nesting-control-button_visibility_hidden {
  visibility: hidden;
}

</style>