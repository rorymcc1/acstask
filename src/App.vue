<template>
  <div id="app">
    <h1>Test Results</h1>
    <button v-if="panels.length > 0" class="btn btn-info" v-on:click="refreshData">
      Refresh Lists
    </button>
    <button v-if="panels.length == 0" class="btn btn-success" v-on:click="refreshData">
      Generate Lists
    </button>
    <div class="card" v-for="panel in panels">
      <div class="card-header bg-info">
        <div class="row">
          <div class="col-sm-6">
            <h2 class="text-white">{{ panel.name }} ({{ panel.abbreviation }}) {{ panel.identifier }}</h2>
            <p>{{ panel.description }}</p>
          </div>
          <div class="col-sm-6">
            <h6 class="text-white">Created At: {{ panel.created_at }}</h6>
            <h6 class="text-white">Updated At: {{ panel.updated_at }}</h6>
          </div>
        </div>
      </div>
      <div class="card-block p-3">
        <div class="row list p-2" v-for="test in tests" v-if="(panel.id == test.panel_id)?true:false">
          <div class="col-sm-5">
              <h6><b class="text-info">Name: </b>{{ test.name }}</h6>
              <h6><b class="text-info">Alias: </b>{{ test.alias }}</h6>
              <h6><b class="text-info">Abbreviation: </b>{{ test.abbreviation }}</h6>
              <h6><b class="text-info">Identifier: </b>{{ test.identifier }}</h6>
          </div>
          <div class="col-sm-3">
            <h6><b class="text-info">Low Value: </b>{{ test.low_value }}</h6>
            <h6><b class="text-info">High Value: </b>{{ test.high_value }}</h6>
          </div>
          <div class="col-sm-4">
            <h6><b class="text-info">Created At: </b><br/>{{ test.created_at }}</h6>
            <h6><b class="text-info">Updated At: </b><br/>{{ test.updated_at }}</h6>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

  import axios from "axios";

  export default {
    name: 'app',
    data () {
      return {
          panels: "",
          tests: "",
      }
    },
    mounted() {},
    methods: { 
      refreshData: function() {
        axios({ method: "GET", "url": "http://challenge.acslabtest.com/api/lab/tests" }).then(result => {
            this.tests = result.data;
          }, error => {
            console.error(error);
          });

        axios({ method: "GET", "url": "http://challenge.acslabtest.com/api/lab/panels" }).then(result => {
            this.panels = result.data;
          }, error => {
            console.error(error);
          });
        }
    }
  }

</script>

