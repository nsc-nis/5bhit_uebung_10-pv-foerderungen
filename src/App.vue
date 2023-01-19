<template>
  <div id="app">
    <Funding @bewilligtEvent="updateBewilligt" @zaehlpunktEvent="updateZaehlpunkt"
        :data="data"
        :max="maxFunding"
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
    const data = ref(pvData);
    const maxFunding = 10000000;

    function updateBewilligt(index) {
      console.log('[ OK ] Index: ' + index);
      console.log('[ OK ] Data: ');
      console.log(data.value);

      data.value[index].bewilligt = !data.value[index].bewilligt;

      console.log('[ CHANGED ] Data: ');
      console.log(data.value);
    }

    function updateZaehlpunkt(index, value)
    {
      console.log('[ OK ] Index: ' + index);
      console.log('[ OK ] Data: ');
      console.log(data.value);

      data.value[index].zaehlpunkt = value;

      console.log('[ CHANGED ] Data: ');
      console.log(data.value);

      return false;
    }

    return { data, maxFunding, updateBewilligt, updateZaehlpunkt };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
