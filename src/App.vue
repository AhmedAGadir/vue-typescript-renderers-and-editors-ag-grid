

<template>
  <ag-grid-vue
    style="width: 500px; height: 300px;"
    class="ag-theme-alpine"
    :columnDefs="columnDefs"
    :rowData="rowData"
  ></ag-grid-vue>
</template>

<script>
/* eslint-disable vue/no-unused-components */

import { AgGridVue } from "ag-grid-vue";
import MyRenderer from "./components/MyRenderer.vue";
import MyEditor from "./components/MyEditor.vue";

export default {
  name: "App",
  data() {
    return {
      columnDefs: null,
      rowData: null
    };
  },
  components: {
    AgGridVue,
    MyRenderer,
    MyEditor
  },
  beforeMount() {
    this.columnDefs = [
      {
        headerName: "Make (Cell Renderer)",
        field: "make",
        cellRendererFramework: "MyRenderer"
      },
      {
        headerName: "Model (Editable)",
        field: "model",
        cellEditorFramework: "MyEditor",
        editable: true
      },
      { headerName: "Price", field: "price" }
    ];

    this.rowData = [
      { make: "Toyota", model: "Celica", price: 35000 },
      { make: "Ford", model: "Mondeo", price: 32000 },
      { make: "Porsche", model: "Boxter", price: 72000 }
    ];
  }
};
</script>

<style lang="scss">
@import "../node_modules/ag-grid-community/dist/styles/ag-grid.css";
@import "../node_modules/ag-grid-community/dist/styles/ag-theme-alpine.css";
</style>
