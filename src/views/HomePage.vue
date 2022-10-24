<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>To do List</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-input placeholder="Enter company name" id="input_field"></ion-input>
      <ion-button v-on:click="getInputValue()">"Salva"</ion-button>
      <ion-list>
        <ion-item v-for="i in input_list" :key="i">
          <ion-label>
            {{ i }}
            <ion-button v-on:click="elimina(i)">Elimina</ion-button>
          </ion-label>
        </ion-item>
      </ion-list>
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
    getInputValue: function () {
      const input_element = document.querySelector("#input_field")
      input_element.value === '' ? alert("valore di input vuoto") : this.input_list.push(input_element.value)
      input_element.value = ""
    },
    elimina: function (el) {
      const index = this.input_list.indexOf(el)
      const length = this.input_list.length
      if (index === 0){
        this.input_list.shift()
      } else if (index === length - 1){
        this.input_list.pop()
      } else{
        const new_input_list = []
        for(let i = 0; i < length; i++){
          if(i !== index){
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
#container {
  text-align: center;

  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;

  color: #8c8c8c;

  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
