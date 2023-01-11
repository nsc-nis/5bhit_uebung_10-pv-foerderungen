<template>
  <h1>Bisherige Ansuchen (Max. Fördersumme: {{ max }}€)</h1>
  <table>
    <thead>
    <tr><td><b>Name</b></td><td><b>PLZ.</b></td><td><b>Zählpunkt</b></td><td><b>kW peak</b></td><td><b>Bewilligt</b></td></tr>
    </thead>
    <tbody>
    <tr v-for="(item, index) in data">
      <td>{{ item.name }}</td><td>{{ item.plz }}</td><td>{{ item.zaehlpunkt }}</td><td>{{ item.kwPeak}}</td><td><input type="checkbox" :checked="item.bewilligt" @change="updateBewilligung(index)"></td>
    </tr>
    </tbody>
    </table>
</template>

<script>
export default
{
  props: {
    data: { type: Array, required: true },
    max: {type: Number, required: true},
    updateBewilligung: {type: Function, required: true},
  },
};
</script>

<style scoped>
*
{
  margin: auto;
}
thead
{
  background-color: #41B883;
}
thead tr
{
  background-color: #41B883;
}
table {
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
}
td,
th {
  border: 1px solid #ddd;
  padding: 8px;
}
tr {
  background-color: #f2f2f2;
}
tbody tr:hover {
  background-color: #ddd;
}
th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #41b883;
  color: white;
}
</style>
