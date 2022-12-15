<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <ion-fab>
        <ion-fab-button @click="printCurrentPosition()" >
          <ion-icon :icon="map"></ion-icon
        ></ion-fab-button>
      </ion-fab>
      <br>
      <br>
      <br>
      <br>  
      <div v-html="Latitude"></div>
      <div v-html="Longitude"></div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { Geolocation } from "@capacitor/geolocation";
import { defineComponent, ref } from "vue";
import { map } from "ionicons/icons";
import { IonPage, IonContent } from "@ionic/vue";

export default defineComponent({
  name: "Tab1Page",
  components: {
    IonContent,
    IonPage,
  },
  setup() {
    let Latitude = ref("<b>Latitude:</b> ");
    let Longitude = ref("<b>Longitude:</b> ");
    const printCurrentPosition = async () => {
      const coordinates = await Geolocation.getCurrentPosition();
      Latitude.value += coordinates.coords.latitude;
      Longitude.value += coordinates.coords.longitude;
      console.log("Current position:", coordinates);
    };
    return {
      printCurrentPosition,
      Latitude,
      Longitude,
      map,
    };
  },
});
</script>
