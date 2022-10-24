<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>To do List</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-item id="input_container">
        <ion-input placeholder="Enter company name" id="input_field"></ion-input>
        <ion-button v-on:click="getInputValue()">"Salva"</ion-button>
      </ion-item>
      <ion-item id="list_container">
        <ion-list>
          <ion-item v-for="i in input_list" :key="i">
            <ion-label id="component">
              <h1>{{ i }}</h1>
              <ion-button v-on:click="elimina(i)">Elimina</ion-button>
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
      input_list: ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l"]
    }
  },
  methods: {
    getInputValue: function () {
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
    }
  }
});

</script>

<style scoped>
ion-content{
  margin: 0;
  padding: 0;
  height: 100vh;
  display: grid;
  grid-template-rows: 1fr 2fr;
}

#input_container ion-input{
  height: 60px;
}

#input_container ion-button{
  height: 40px;
  width: 70px;
}

ion-list{
  width: 100vw;
  padding: 0;
  margin: 0;
}

#component{
  display: grid;
  grid-template-columns: 2fr 1fr;
}
</style>
