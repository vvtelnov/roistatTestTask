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
  methods: {
    togglePopup() {
      this.popupOpened = !this.popupOpened;
    },
    addNewPhonebookRow({ name, phone, parent }, currPhoneBookRows = this.phoneBookRows) {
      // console.log(name, name, parent)
      if (parent === null) {
        console.log(name, phone, parent)
        this.phoneBookRows.push({
          name,
          phone,
          nested: [],
        })
      } else {
        // console.log(parent.arrIndex)
        if ((currPhoneBookRows[parent.arrIndex]) && (currPhoneBookRows[parent.arrIndex].name === parent.name)) {
          currPhoneBookRows[parent.arrIndex].nested.push({
            name,
            phone,
            nested: [],
          })
        } else {
            for (let i = 0; i < currPhoneBookRows.length; i++) {
              if (this.phoneBookRows[i].nested.length > 0) {
                // console.log(name, name, parent)
                console.log(currPhoneBookRows[i].nested)
                //   console.log(this.phoneBookRows[0]);
                //   console.log(this.phoneBookRows[0].nested);
                // }
                // console.log(this.phoneBookRows[0].nested.length > 0)
                this.addNewPhonebookRow({name, phone, parent}, currPhoneBookRows[i].nested);
              }
            }
          
        // console.log(this.phoneBookRows);
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
          // console.log(row)
          // this.phoneBookNamesAndId.push({
          //   name: row.name,
          //   id: index,
          // })
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
