<template>
  <div class="popup-overlay">
    <div class="popup">
      <div class="popup__title-container">
        <h3 class="popup__title">{{ popupTitle }}</h3>
        <CloseButton
          class="popup__close-btn"
          v-if="hasCloseBtn"
          @click="closePopup"
        />
      </div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
import CloseButton from './CloseButton.vue';

export default {
  components: { CloseButton },
  props: {
    popupTitle: {
      type: String,
      required: true,
    },
    hasCloseBtn: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    closePopup() {
      this.$emit('closePopup');
    },
  }
}
</script>

<style scoped>
.popup-overlay {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 128, 128, 0.352);
}

.popup {
  position: relative;
  width: 430px;
  background-color: rgb(255, 255, 255);
  box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.15);
  border-radius: 10px;
}

.popup__title-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 10px 15px;
}

.popup__title {
  font-size: 24px;
  line-height: 1.6;
  font-weight: 500;
}

@media screen and (max-width: 480px) {
  .popup-overlay {
    background-color: rgba(0, 128, 128, 0.48);
  }
  .popup {
    width: 100%;
  }

  .popup__title {
    font-size: 32px;
    line-height: 1.2;
    text-align: center;
  }

  .popup__close-btn {
    position: relative;
    top: -80px;
    left: -10px;
    background-color: rgba(0, 128, 128, 0);
    font-size: 40px;
  }
}
</style>
