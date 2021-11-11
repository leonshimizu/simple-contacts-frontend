<template>
  <div class="home">
    <h1>{{ message }}</h1>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data: function() {
    return {
      message: "Hello World"
    }
  }
};
</script>