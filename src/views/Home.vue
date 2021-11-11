<template>
  <div class="home">
    <!-- <h1>{{ contacts }}</h1> -->
    <h1>Here are all the contacts:</h1>
    <button v-on:click="createFunction()">Add Contact</button>
    <ul>
      <li v-for="contact in contacts">
       {{ contact.id }}
       {{ contact.first_name }} {{ contact.last_name }}
       <button v-on:click="showFunction(contact)">Show More Info</button>
      </li>
    </ul>
    <dialog id="show-modal">
      <form method="dialog">
        <p>First Name: <input type="text" v-model="currentContact.first_name"></p>
        <p>Last Name: <input type="text" v-model="currentContact.last_name"></p>
        <p>Phone Number: <input type="text" v-model="currentContact.phone_number"></p>
        <p>Email: <input type="text" v-model="currentContact.email"></p>
        <button v-on:click="updateFunction(currentContact)">Update</button>
        <button>Close</button>
      </form>
    </dialog>
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
      contacts: [],
      currentContact: {}
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
    showFunction: function(theContact) {
      console.log("in the show function");
      this.currentContact = theContact;
      document.querySelector("#show-modal").showModal();
      console.log(theContact.first_name);
    },
    updateFunction: function(theContact) {
      console.log("in the update function");
      console.log(theContact.first_name)
      axios
        .patch(`http://localhost:3000/contacts/1.json`, {
          first_name: theContact.first_name,
          last_name: theContact.last_name,
          phone_number: theContact.phone_number,
          email: theContact.email
        })
        .then(response => {
          console.log(response.data);
        })
    }
  }
};
</script>