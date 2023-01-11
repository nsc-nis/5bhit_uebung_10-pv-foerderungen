<template>
  <div id="app">
    <Funding
        :data="data"
        :max="maxFunding"
        :updateBewilligung="updateBewilligt"
    />
  </div>
</template>

<script>
import Funding from './components/Funding.vue';
import pvData from "./data.json"
import { ref } from 'vue';

export default {
  name: 'App',
  components: {
    Funding,
  },
  setup() {
    const data = ref(pvData);/*ref([
      {
        name: 'Maier',
        plz: '4020',
        zaehlpunkt: '0000-5232-4199-1234-0983',
        kwPeak: 14.4,
        bewilligt: true,
      },
      {
        name: 'Huber',
        plz: '4620',
        zaehlpunkt: '0000-1232-4189-1124-1983',
        kwPeak: 10.0,
        bewilligt: false,
      },
      {
        name: 'Rager',
        plz: '4400',
        zaehlpunkt: '0450-9832-4109-1764-1999',
        kwPeak: 19.0,
        bewilligt: false,
      },
    ]);
    */
    const maxFunding = 10000000;

    function updateBewilligt(index) {
      console.log('[ OK ] Index: ' + index);
      console.log('[ OK ] Data: ');
      console.log(data.value);

      data.value[index].bewilligt = !data.value[index].bewilligt;

      console.log('[ CHANGED ] Data: ');
      console.log(data.value);
    }

    return { data, maxFunding, updateBewilligt };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
