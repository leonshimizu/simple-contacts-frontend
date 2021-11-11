<template>
  <div class="home">
    <!-- <h1>{{ contacts }}</h1> -->
    <ul>
      <li v-for="contact in contacts">
       {{ contact.id }}
       {{ contact.first_name }} {{ contact.last_name }}
       {{ contact.email }}
       {{ contact.phone_number }}
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
    }
  }
};
</script>