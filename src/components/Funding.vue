<template>
  <div>
    <h1>PV - Fördererungen</h1>
    EAG-Investitionszuschuss Photovoltaik und Stromspeicher im Jahr 2023<br>
    Mit dem Erneuerbaren-Ausbau-Gesetz (EAG) wurden die rechtlichen Rahmenbedingungen für den Netzanschluss von erneuerbaren Energieanlagen vereinfacht. Dies umfasst auch finanzielleErleichterungen in Form eines pauschalierten Netzzutrittsentgelts. Mit einem der EAG-Investitionszuschüsse werden die Neuerrichtung und Erweiterung von Photovoltaikanlagen und die damit verbundene Neuerrichtung von Stromspeichern gefördert. Für die Erweiterung einer Photovoltaikanlage ist keine Mindestgröße vorgesehen.
  </div>
  <div>
    <h2>Bisherige Ansuchen (Max. Fördersumme: {{ max }}€)</h2>
  </div>
  <table>
    <thead>
    <tr><td><b>Name</b></td><td><b>PLZ.</b></td><td><b>Zählpunkt</b></td><td><b>kW peak</b></td><td><b>Bewilligt</b></td></tr>
    </thead>
    <tbody>
    <tr v-for="(item, index) in data" :key="index">
      <td>{{ item.name }}</td><td>{{ item.plz }}</td><td v-if="!editingActive" @click="activateEditing()">{{ item.zaehlpunkt }}</td><td v-else><input id="textField_zaehlpunkt" type="text"  :value="item.zaehlpunkt" @change="updateIndexValue(index)"></td><td>{{ item.kwPeak}}</td><td><input type="checkbox" :checked="item.bewilligt" @change="$emit('bewilligtEvent', index)"></td><!--"updateBewilligung(index)"-->
    </tr>
    </tbody>
  </table>
  <div v-if="editingActive">
    <button @click="editingActive = updateZaehlpunkt(indexInput, valueInput)">Save</button>
    <button @click="cancelEditing">Cancel</button>
  </div>
</template>

<script>
import { ref } from 'vue';
export default
{
  props: {
    data: { type: Array, required: true },
    max: {type: Number, required: true},
    /*updateBewilligung: {type: Function, required: true},*/
    /*updateZaehlpunkt: { type: Function, required: true},*/
  },
  setup(props, context)
  {
    const editingActive = ref(false);//ref(false);
    const indexInput = ref();
    const valueInput = ref();

    function activateEditing()
    {
      editingActive.value = true;
      console.log(editingActive);
    }

    function updateIndexValue(index)
    {
      indexInput.value = index;
      valueInput.value = document.getElementById("textField_zaehlpunkt").value;
      console.log("[ OK ] indexInput: " + indexInput.value);
      console.log("[ OK ] valueInput: " + valueInput.value);
    }

    function cancelEditing()
    {
      editingActive.value = false;
    }

    function updateZaehlpunkt()
    {
      editingActive.value = false;

      context.emit('zaehlpunktEvent', indexInput.value, valueInput.value);
    }

    return { editingActive, activateEditing, cancelEditing, updateIndexValue, updateZaehlpunkt }
  }
};
</script>

<style scoped>

*
{
  text-align: left;
}
div
{
  text-align: left;
  margin-top: 0;
  margin-left: 2em;
  margin-right: 2em;
  margin-bottom: 2em;
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
  margin-top: 0;
  margin-left: 2em;
  margin-right: 2em;
  margin-bottom: 0.25em;
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
button
{
  margin-top: 0.25em;
  margin-left: 0.25em;
  margin-right: 0.25em;
}
</style>
