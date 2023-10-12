<template>
    <FullscreenPopup
      :popupTitle="'Добавление пользователя'"
      :hasCloseBtn="true"
    >
      <form class="add-users-form" @submit.prevent="submitForm">

        <div class="add-users-form__input-container">
          <label class="add-users-form__label" for="name-input">Имя</label>
          <input
            class="add-users-form__input"
            id="name-input"
            type="text"
            v-model="formInputs.name"
          >
        </div>

        <div class="add-users-form__input-container">
          <label class="add-users-form__label" for="phone-input">Телефон</label>
          <input 
            class="add-users-form__input"
            id="phone-input" 
            type="text" 
            v-model="formInputs.phone"
          >
        </div>

        <div class="add-users-form__input-container">
          <label class="add-users-form__label" for="parent-input">Начальник</label>
          <select
            class="add-users-form__input"
            id="parent-input"
            v-model="formInputs.parent"
          >
            <option :value="null">Нет начальника</option>
            <option
              v-for="(option, index) in phoneBookNamesAndId"
              :key="index"
              :value="{
                name: option.name, 
                arrIndex: option.id,
              }"
            >{{ option.name }}</option>
          </select>
        </div>

        <DefaultButton class="from__submit-btn">Сохранить</DefaultButton>
      </form>
    </FullscreenPopup>
</template>

<script>
import FullscreenPopup from './UI/FullscreenPopup.vue';
import DefaultButton from './UI/DefaultButton.vue';

export default {
  components: { FullscreenPopup, DefaultButton },
  data() {
    return {
      formInputs: {
        name: '',
        phone: '',
        parent: null,
      }
    }
  },
  props: {
    phoneBookNamesAndId: {
      type: Array,
      required: true,
    }
  },
  methods: {
    submitForm() {
      this.$emit('addNewPhonebookRow', this.formInputs);
      this.$emit('closePopup');
      this.formInputs = {
        name: '',
        phone: '',
        parent: null,
      };
    },
  }
}

</script>

<style scoped>
.add-users-form {
  padding: 10px 15px;
  width: 100%;
  min-height: 200px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

.add-users-form__input-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-bottom: 20px;
}

.add-users-form__input-container:last-of-type {
  margin-bottom: 0px;
}

.add-users-form__label {
  font-size: 16px;
  line-height: 1.8;
}
.add-users-form__input {
  width: 250px;
  height: 25px;
  font-size: 16px;
}

.from__submit-btn {
  margin-top: 40px;
  align-self: flex-start;
}

@media screen and (max-width: 480px) {
  .add-users-form {
    margin: auto;
  }
  .add-users-form__input-container {
    flex-direction: column;
    margin-bottom: 30px;
  }

  .add-users-form__label {
    font-size: 18px;
    color: rgba(0, 0, 0, 0.683);
  }

  .add-users-form__input {
    width: 100%;
    height: 30px;
    font-size: 18px;
  }

  .from__submit-btn {
    width: 100%;
  }
}
</style>