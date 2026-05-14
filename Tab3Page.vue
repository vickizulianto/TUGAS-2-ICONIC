<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Cuaca Jakarta</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <div id="container">
        <table class="center" v-if="weatherData && weatherData.hourly">
          <tr>
            <th>Waktu</th>
            <th>Temperatur (°C)</th>
          </tr>
          <tr
            v-for="(temp, index) in weatherData.hourly.temperature_2m.slice(
              0,
              24,
            )"
            :key="index"
          >
            <td>{{ weatherData.hourly.time[index] }}</td>
            <td>{{ temp }}°C</td>
          </tr>
        </table>
        <p v-else-if="error">{{ error }}</p>
        <p v-else>Loading...</p>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonHeader,
  IonPage,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";
import { onMounted } from "vue";
import { weatherData, error, fetchWeather } from "@/services/EndPointAccess";

onMounted(fetchWeather);
</script>

<style scoped>
.center {
  margin: auto;
  width: 50%;
  border-collapse: collapse;
}

th,
td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}
</style>
