<script>

import FilesViewer from "./components/FilesViewer";
import NodeList from "./components/NodeList"
import Button from "./components/Button";

export default {
  components: { FilesViewer, Button, NodeList },
  data() {
    return {
      openFileViewer: false,
    };
  },

  methods: {
    toggleOpenFileViewer() {
      this.openFileViewer = !this.openFileViewer;
    },
  },
};
</script>

<template>
  <Button text="Open File" color="green" @btn-click="toggleOpenFileViewer" />

  <FilesViewer
    v-show="openFileViewer"
  />

  <NodeList />
</template>