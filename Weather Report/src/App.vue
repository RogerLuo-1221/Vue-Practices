<script setup>
import axios from 'axios'
import { ref } from 'vue'

const city = ref('')
const forecasts = ref([])

function get_weather() {
  axios.get('http://wthrcdn.etouch.cn/weather_mini?city=' + city.value)
  .then(function(response){
    forecasts.value = response.data.data.forecast;
    console.log(response.data.data.forecast);
  });
  city.value = '';
}
function change_city(location) {
  city.value = location;
  get_weather();
}
</script>

<template>
  <div class="wrap" id="app">
    <div class="search_form">
      <input 
        type="text" 
        v-model="city" 
        class="input_txt" 
        @keyup.enter="get_weather()"
      />
      <button class="input_sub" @click="get_weather()">
        Search
      </button>
      <div class="hotkey">
        <a href="javascript:;" @click="change_city('北京')">北京</a>
        <a href="javascript:;" @click="change_city('上海')">上海</a>
        <a href="javascript:;" @click="change_city('广州')">广州</a>
        <a href="javascript:;" @click="change_city('深圳')">深圳</a>
      </div>
    </div>
    <ul class="weather_list">
      <li v-for="item in forecasts">
        <div class="info_type">
          <span class="iconfont">
            {{ item.type }}
          </span>
        </div>
        <div class="info_temp">
          <b>{{ item.low }}</b>
          ~
          <b>{{ item.high}}</b>
        </div>
        <div class="info_date">
          <span>
            {{ item.date }}
          </span>
        </div>
      </li>
    </ul>
  </div>
</template>

<style>
  @import "./assets/style.css";
</style>