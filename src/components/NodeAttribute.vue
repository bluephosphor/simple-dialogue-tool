<script>
export default {
  props: {
    name: String,
    attribute: String,
    editing: Boolean,
  },
  data() {
    return {
      value: this.attribute,
    };
  },
};
</script>
<template>
  <tr class="attribute">
    <td class="label">{{ this.name }}:</td>
    <td v-if="this.editing">
      <input v-model="this.value" class="text-input" :placeholder="this.name" />
    </td>
    <td v-else class="card-text">{{ this.value }}</td>
  </tr>
</template>

<style scoped>

.text-input {
  font-family: monospace;
  background: black;
  color: white;
  border: 1px solid white;
  width: 98%;
  height: 100%
}

td{
    padding: 4px;
    margin: 16px 0px;
    height: 24px;
}

.label{
    width:20%;
}
</style>