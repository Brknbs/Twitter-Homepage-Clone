<template>
  <div id="app" class="flex container h-screen w-full">
    <Navbar />
    <Tweets />
    <Trendings />
  </div>
</template>

<script>
import Navbar from './components/Navbar';
import Tweets from './components/Tweets';
import Trendings from './components/Trendings';

export default {
  name: 'App',
  components: {
    Navbar,
    Tweets,
    Trendings
  },
  data() {
    return {
      
    }
  },
  
}
</script>

<style lang="scss">

</style>
