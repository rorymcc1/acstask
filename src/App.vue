<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <testList msg="Welcome to ACS Code Challenge using Vue.js" />
      <h1>Your IP is {{ ip }}</h1>
      <input type="text" v-model="input.firstname" placeholder="First Name" />
      <input type="text" v-model="input.lastname" placeholder="Last Name" />
      <button v-on:click="sendData()">Send</button>
      <br />
      <br />
      <textarea>{{ response }}</textarea>
  </div>
</template>

<script>
import testList from "./components/testList.vue";

import axios from "axios";

export default {
  name: 'app',
  data () {
      return {
          ip: "",
          input: {
            firstname: "",
            lastname: ""
          },
          response: ""
      }
  },
  mounted() { 
    axios({ method: "GET", "url": "https://httpbin.org/ip" }).then(result => {
        this.ip = result.data.origin;
      }, error => {
        console.error(error);
      });
  },
  methods: { 
    sendData() {
      axios({ method: "POST", 
              "url": "https://httpbin.org/post", 
              "data": this.input, 
              "headers": { "content-type": "application/json" } 
            }).then(result => {
        this.response = result.data;
      }, error => {
          console.error(error);
      });
    }
  }
}

// export default {
//   name: "app",
//   components: {
//     testList
//   }
// };

</script>

