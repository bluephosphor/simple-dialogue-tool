<script>
import Button from "./Button";

export default {
  name: "DialogueNode",
  components: {
    Button,
  },
  props: {
    nodeData: Object,
  },
  data() {
    return {
      editing: false,
      type: this.nodeData.type,
      speaker: this.nodeData.speaker,
      text: this.nodeData.text,
      event: this.nodeData.event,
    };
  },
  methods: {
    toggleEdit() {
      this.editing = !this.editing;
    },
  },
};
</script>

<template>
  <div class="card">
    <div class="card-body">
      <p class="label">speaker:</p>
      <input
        v-if="this.editing"
        v-model="this.speaker"
        class="text-input"
        placeholder="text"
      />
      <p v-else class="card-text">{{ this.speaker }}</p>

      <p class="label">text:</p>
      <input
        v-if="this.editing"
        v-model="this.text"
        class="text-input"
        placeholder="text"
      />
      <p v-else class="card-text">{{ this.text }}</p>

      <p class="label">event:</p>
      <input
        v-if="this.editing"
        v-model="this.event"
        class="text-input"
        placeholder="text"
      />
      <p v-else class="card-text">{{ this.event }}</p>
    </div>
    <Button
      :text="this.editing ? 'Save' : 'Edit'"
      color="blue"
      @click="toggleEdit"
    />
  </div>
</template>

<style scoped>
.card {
  width: 40%;
  border: 1px solid gray;
  border-radius: 5px;
  font-family: monospace;
  margin: 16px 8px;
  padding: 8px;
}

.card-body{
    display: grid;
  grid-template-rows: auto auto;
  grid-template-columns: auto auto;
}

.attribute {
  display: flex;
}

.text-input {
  font-family: monospace;
  background: black;
  color: white;
  border: 1px solid white;
  padding: 4px;
  margin: 8px 0px;
  width: 90%;
}
</style>