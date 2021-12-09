<script>
import NodeAttribute from "./NodeAttribute"
import Button from "./Button";

export default {
  name: "DialogueNode",
  components: {
    NodeAttribute,
    Button
  },
  props: {
    nodeData: Object,
  },
  data() {
    return {
      editing:  false,
      type:     this.nodeData.type,
      speaker:  this.nodeData.speaker,
      text:     this.nodeData.text,
      event:    this.nodeData.event,
    };
  },
  methods:{
      toggleEdit(){
          this.editing = !this.editing
      }
  }
};
</script>

<template>
  <table class="card">
    <tbody class="card-body">
      <NodeAttribute name="speaker" :attribute="this.speaker"   :editing="this.editing"/>
      <NodeAttribute name="text"    :attribute="this.text"      :editing="this.editing"/>
      <NodeAttribute name="event"   :attribute="this.event"     :editing="this.editing"/>
    </tbody>
    <Button
      :text="this.editing ? 'Save' : 'Edit'"
      color="blue"
      @click="toggleEdit"
    />
  </table>
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


</style>