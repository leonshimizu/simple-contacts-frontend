<template>
  <div class="home">
    <!-- <h1>{{ contacts }}</h1> -->
    <h1>Here are all the contacts:</h1>
    <button v-on:click="createFunction()">Add Contact</button>
    <ul>
      <li v-for="contact in contacts">
       {{ contact.id }}
       {{ contact.first_name }} {{ contact.last_name }}
       {{ contact.email }}
       {{ contact.phone_number }}
       <button v-on:click="showFunction()">Show More Info</button>
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data: function() {
    return {
      message: "Hello World",
      contacts: []
    }
  },
  created: function() {
    this.indexFunction();
  },
  methods: {
    indexFunction: function() {
      console.log("in the index function");
      axios
        .get('http://localhost:3000/contacts')
        .then(response => {
          console.log(response.data);
          this.contacts = response.data;
        })
    },
    createFunction: function() {
      console.log("in the create function");
      axios 
        .post('http://localhost:3000/contacts.json', {
          first_name: "Stassie",
          last_name: "Shimizu",
          email: "stassie@gmail.com",
          phone_number: "0987654321"
        }).then(response => {
          console.log(response.data);
          this.contacts.push(response.data);
        })
    },
    showFunction: function() {
      console.log("in the show function");
      // document.querySelector
    }
  }
};
</script>