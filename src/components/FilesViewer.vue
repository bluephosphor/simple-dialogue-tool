<script>
import fs from "fs";
import pathModule from "path";
import { app } from "@electron/remote";
import { computed, ref } from "vue";

import IconFile from "./IconFile";
import IconFolder from "./IconFolder";
import IconFolderOpen from "./IconFolderOpen";

const formatSize = (size) => {
  var i = Math.floor(Math.log(size) / Math.log(1024));
  return (
    (size / Math.pow(1024, i)).toFixed(2) * 1 +
    " " +
    ["b", "kb", "mb", "gb", "tb"][i]
  );
};

export default {
  props: {
    files: { type: Array, default: () => [] },
  },
  components: { IconFile, IconFolder, IconFolderOpen },
  setup() {
    const path = ref(app.getAppPath());
    const filesList = computed(() => {
      const fileNames = fs.readdirSync(path.value);
      return fileNames
        .map((file) => {
          const stats = fs.statSync(pathModule.join(path.value, file));
          return {
            name: file,
            size: stats.isFile() ? formatSize(stats.size ?? 0) : null,
            directory: stats.isDirectory(),
          };
        })
        .sort((a, b) => {
          if (a.directory === b.directory) {
            return a.name.localeCompare(b.name);
          }
          return a.directory ? -1 : 1;
        });
    });

    const back = () => {
      path.value = pathModule.dirname(path.value);
    };
    const open = (folder) => {
      path.value = pathModule.join(path.value, folder);
    };

    const searchString = ref("");
    const filteredFiles = computed(() => {
      return searchString.value
        ? filesList.value.filter((s) => s.name.startsWith(searchString.value))
        : filesList.value;
    });

    const onFileClick = (file) => {
      if (file.directory) open(file.name);
    };

    return {
      path,
      open,
      back,
      filesList,
      searchString,
      filteredFiles,
      onFileClick,
    };
  },
};
</script>

<template>
  <div>
    <div class="container mt-2">
      <h4>{{ path }}</h4>

      <div class="form-group mt-4 mb-2">
        <input
          v-model="searchString"
          class="form-control form-control-sm"
          placeholder="File Search"
        />
      </div>
    </div>

    <table class="table">
      <tbody>
        <tr class="clickable" @click="back">
          <td class="icon-row">
            <IconFolderOpen class="icon-folder" />
          </td>
          <td>...</td>
          <td></td>
        </tr>

        <tr
          v-for="file in filteredFiles"
          :key="file.name"
          :class="{ clickable: file.directory }"
          @click="onFileClick(file)"
        >
          <td class="icon-row">
            <IconFolder v-if="file.directory" class="icon-folder" />
            <IconFile v-else class="icon-file" />
          </td>
          <td>{{ file.name }}</td>
          <td>
            <span class="float-end">{{ file.size }}</span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
*{
    font-family: sans-serif;
}

.clickable {
  cursor: pointer;
}
.icon-row {
  width: 2em;
}
.icon-folder {
  width: 1em;
}
.icon-file {
  width: 0.75em;
}
</style>