<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import countries from '/src/countries.json';
import { defineProps } from 'vue';


const { alpha3Code } = defineProps({
  alpha3Code: String,
});


const route = useRoute();
const country = ref({});
let alpha3Small = ''; 
let bigFlag = "";

onMounted(() => {
  const alpha3Code = route.params.alpha3Code;
  alpha3Small = alpha3Code.toLowerCase();
  const countryData = countries.find((country) => country.alpha3Code === alpha3Code);
  if (countryData) {
    country.value = countryData;
  } else {
    // Handle the case when country data is not found
    console.error(`Country data not found for alpha3Code: ${alpha3Code}`);
  }
  
});


bigFlag = "https://restcountries.eu/data/" + alpha3Code + ".svg"
//the object item for the flag is missing in the provided dataset. It is only available when accessing the API
console.log("Bigflag URL: " + bigFlag)
</script>

<template>
  <!-- Country Details (Bootstrap column) -->
  <div class="col-7" v-show="country.name">
    <img :src=bigFlag alt="country flag" style="width: 300px"/>
    <h1>{{ country.name?.common }}</h1>
    <table class="table">
      <thead></thead>
      <tbody>
        <tr>
          <td style="width: 30%">Capital</td>
          <td>{{ country.capital}}</td>
        </tr>
        <tr>
          <td>Area</td>
          <td>
            {{ country.area }} km <sup>2</sup>
          </td>
        </tr>
        <tr>
          <td>Borders</td>
          <td>
            <ul>
              <li v-for="border in country.borders" :key="border">
                <router-link :to="`/${border}`">{{ border }}</router-link>
              </li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  <div v-show="!country.name">
    <!-- Display a loading message or an error message when country data is not found -->
    <p>Loading country data...</p>
  </div>
</template>


<style>

</style>
