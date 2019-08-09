<template>
  <div class="home">
    
 Github Search
    <form @submit.prevent="userSearch(userInput)">
      {{ userInput }}
      <input v-model="userInput" />
      <div v-if="response">Name: {{ response.name }}</div>
      <div v-if="response">User Name: {{ response.login }}</div>
      <div v-if="response">Id: {{ response.id }}</div>
      {{response}}
    </form>
  </div>
</template>
<script>
import Vue from "vue";
import axios from "axios";
export default Vue.extend({
  name: "home",
  data() {
    return {
      userInput: "",
      uri: "https://api.github.com/users/",
      response: ''
    };
  },
  methods: {
    userSearch(userInput) {
      axios.get(`${this.$data.uri}${userInput}`)
        .then((response) => {
          // handle success
          this.$data.response = response.data;
        })
        .catch((error) => {
          // handle error
          console.log(error);
        })
    }
  }
});
</script>

