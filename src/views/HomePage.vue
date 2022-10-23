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
        <ion-item v-for="i in input" :key="i">
          <ion-label>{{i}}</ion-label>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="js">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton, IonInput, IonList, IonItem, IonLabel} from '@ionic/vue';
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
  data(){
    return{
      input: []
    }
  },
  methods: {
    getInputValue: function(){
      const input_element = document.querySelector("#input_field")
      this.input.push(input_element.value) 
      input_element.value = ""
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
