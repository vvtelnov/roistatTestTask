<template>
  <div id="app">
    <div class="phone-book">
      <DefaultButton
        class="phone-book__add-btn"
        @click="togglePopup"
      >Добавить</DefaultButton>
      <PhoneBook
        class="phone-book__table"
        :phoneBookRows=phoneBookRows
      />
    </div>
    <PopupForm
      v-show="popupOpened"
      @closePopup="togglePopup"
      @addNewPhonebookRow="addNewPhonebookRow"
      :phoneBookNamesAndId="phoneBookNamesAndId"
    />
  </div>
</template>

<script>
import PopupForm from './components/PopupForm.vue';
import PhoneBook from './components/PhoneBook.vue';
import DefaultButton from './components/UI/DefaultButton.vue';

export default {
  components: { PopupForm, PhoneBook, DefaultButton },
  data() {
    return {
      phoneBookRows: [],
      popupOpened: false,
      phoneBookNamesAndId: [],
    }
  },
  mounted() {
    this.phoneBookRows = JSON.parse(localStorage.getItem('phoneBookRows')) || [];
    this.phoneBookNamesAndId = JSON.parse(localStorage.getItem('phoneBookNamesAndId')) || [];
  },
  watch: {
    phoneBookRows: {
      handler(updatedPhoneBookRows) {
        localStorage.setItem('phoneBookRows', JSON.stringify(updatedPhoneBookRows));
      },
      deep: true,
    },
    phoneBookNamesAndId: {
      handler(updatedPhoneBookNamesAndId) {
        localStorage.setItem('phoneBookNamesAndId', JSON.stringify(updatedPhoneBookNamesAndId));
      },
      deep: true,
    },
  },
  methods: {
    togglePopup() {
      this.popupOpened = !this.popupOpened;
    },
    addNewPhonebookRow({ name, phone, parent }, currPhoneBookRows = this.phoneBookRows) {
      if (parent === null) {
        this.phoneBookRows.push({
          name,
          phone,
          nested: [],
        })
      } else if ((currPhoneBookRows[parent.arrIndex]) && (currPhoneBookRows[parent.arrIndex].name === parent.name)) {
        currPhoneBookRows[parent.arrIndex].nested.push({
          name,
          phone,
          nested: [],
        })
      } else {
          for (let i = 0; i < currPhoneBookRows.length; i++) {
            if (this.phoneBookRows[i].nested.length > 0) {
              this.addNewPhonebookRow({name, phone, parent}, currPhoneBookRows[i].nested);
            }
          }
        }

      this.phoneBookNamesAndId = [];
      this.updatePhoneBookNamesAndId(this.phoneBookRows);
    },
    updatePhoneBookNamesAndId(phonebookRows) {
      for (let index = 0; index < phonebookRows.length; index++ ) {
        const row = phonebookRows[index];

        this.phoneBookNamesAndId.push({
            name: row.name,
            id: index,
        })

        if ((Array.isArray(row.nested)) && (row.nested.length !== 0)) {
          this.updatePhoneBookNamesAndId(row.nested);
        }
      }
    },
  },
}
</script>

<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.phone-book {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  margin: 40px 0 0 100px;
  max-width: 600px;
}

.phone-book__add-btn {
  margin-bottom: 30px;
  width: 150px;
}

@media screen and (max-width: 820px) {
  .phone-book {
    align-items: center;
    margin: 40px auto 0;
    max-width: 95%;
  }

  .phone-book__add-btn {
    margin-bottom: 45px;
    width: 80%;
  }
}
</style>
