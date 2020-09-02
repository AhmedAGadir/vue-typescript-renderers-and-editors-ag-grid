<template>
  <div>
    <div>Last clicked value: {{lastClickedValue}}</div>
    <ag-grid-vue
      style="width: 500px; height: 300px;"
      class="ag-theme-alpine"
      :columnDefs="columnDefs"
      :rowData="rowData"
      :context="context"
    ></ag-grid-vue>
  </div>
</template>

<script lang="ts">
/* eslint-disable vue/no-unused-components */

import { Component, Vue } from "vue-property-decorator";
import { AgGridVue } from "ag-grid-vue";
import MyRenderer from "./components/MyRenderer.vue";
import MyEditor from "./components/MyEditor.vue";

@Component({
  name: "App",
  components: {
    AgGridVue,
    MyRenderer,
    MyEditor
  }
})
export default class App extends Vue {
  private columnDefs: any = null;
  private rowData: any = null;
  private context = {
    componentParent: this
  };
  private lastClickedValue = null;
  public beforeMount() {
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
  private exec(value: any) {
    this.lastClickedValue = value;
  }
}
</script>

<style lang="scss">
@import "../node_modules/ag-grid-community/dist/styles/ag-grid.css";
@import "../node_modules/ag-grid-community/dist/styles/ag-theme-alpine.css";
</style>
