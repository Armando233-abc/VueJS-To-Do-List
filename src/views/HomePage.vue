<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>To do List</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-item id="input_container">
        <ion-input class="font_testo" placeholder="Scrivi cosa vuoi fare" id="input_field"></ion-input>
        <ion-button class="font_testo" v-on:click="aggiungi()">Salva</ion-button>
      </ion-item>
      <ion-item id="list_container">
        <ion-list>
          <ion-item v-for="i in input_list" :key="i">
            <ion-label id="component">
              <h3 class="font_testo">{{ i }}</h3>
              <ion-button class="font_testo" v-on:click="elimina(i)">X</ion-button>
              <ion-button class="font_testo" v-on:click="fatto(i)">V</ion-button>
            </ion-label>
          </ion-item>
        </ion-list>
      </ion-item>
    </ion-content>
  </ion-page>
</template>

<script lang="js">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton, IonInput, IonList, IonItem, IonLabel } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HomePage',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButton,
    IonInput,
    IonList,
    IonItem,
    IonLabel
  },
  data() {
    return {
      input_list: []
    }
  },
  methods: {
    aggiungi: function () {
      const input_element = document.querySelector("#input_field")
      input_element.value === '' ? alert("valore di input vuoto") : this.input_list.push(input_element.value)
      input_element.value = ""
    },
    elimina: function (el) {
      const index = this.input_list.indexOf(el)
      const length = this.input_list.length
      if (index === 0) {
        this.input_list.shift()
      } else if (index === length - 1) {
        this.input_list.pop()
      } else {
        const new_input_list = []
        for (let i = 0; i < length; i++) {
          if (i !== index) {
            new_input_list.push(this.input_list[i])
          }
        }
        this.input_list = new_input_list
      }
    },
    fatto: function (el) {
      const element = document.querySelectorAll("h3")
      const index = this.input_list.indexOf(el)
      if (element[index].style.textDecorationLine === "line-through"){
        element[index].style.textDecorationLine = "none"
      } else{
        element[index].style.textDecorationLine = "line-through"
      }
    }
  }
});

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Fasthand&family=Lora:ital@1&display=swap');

ion-title {
  font-family: 'Fasthand', cursive;
  font-size: 35px;
  text-align: center;
}

ion-content {
  margin: 0;
  padding: 0;
  height: 100vh;
  display: grid;
  grid-template-rows: 1fr 2fr;
}

.font_testo {
  font-family: 'Lora', serif;
}

#input_container ion-input {
  height: 60px;
  font-size: 20px;
}

#input_container ion-button {
  height: 40px;
  width: 80px;
  font-size: 20px;
}

ion-list {
  width: 100vw;
  padding: 0;
  margin: 0;
}

#component {
  display: grid;
  grid-template-columns: 4fr 0.6fr 0.5fr;
}

#component h3 {
  font-size: 20px;
}

#component ion-button {
  width: 20px;
  font-size: 15px;
}
</style>
