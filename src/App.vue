<script>
import FilesViewer from "./components/FilesViewer";
import NodeList from "./components/NodeList";
import Button from "./components/Button";

import fs from "fs";

export default {
  components: { FilesViewer, Button, NodeList },

  methods: {
    toggleOpenFileViewer() {
      this.openFileViewer = !this.openFileViewer;
    },
    loadExampleData() {
      const p = "./exampledata.json";

      fs.readFile(p, "utf8", (err, data) => {
        if (err) return console.log(err);
        this.convoData = JSON.parse(data);
      });
    },
  },
  data() {
    return {
      openFileViewer: false,
      convoData: [],
    };
  },
};
</script>

<template>
  <Button text="Open File" color="green" @btn-click="toggleOpenFileViewer" />
  <Button text="Open Example Data" color="blue" @btn-click="loadExampleData" />

  <FilesViewer v-show="openFileViewer" />

  <NodeList :nodes="convoData.ROOT" />
</template>

<style>
body {
  background: #101519;
  color: #aaaaaa;
}
</style>