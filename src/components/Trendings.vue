<template>
  <div class="md:block hidden w-1/3 h-full border-l border-lighter py-2 px-6 overflow-y-scroll relative">
    <input type="text" class="rounded-full w-full p-2 bg-lighter focus:outline-none pl-10 text-sm focus:bg-white border focus:border-blue" placeholder="Search Twitter">
    <i class="fas fa-search absolute left-0 top-0 mt-5 ml-10 text-sm text-light"></i>
    <div class="w-full rounded-lg bg-lightest mt-6">
      <div class="flex items-center justify-between px-3 py-1">
        <p class="text-xl font-extrabold">Trends for you</p>
        <div class="hover:bg-lighter rounded-full">
          <i class="fas fa-cog text-lg text-blue cursor-pointer p-3"></i>
        </div>
      </div>
      <button v-for="trend in trending" :key="trend.title" class="w-full flex justify-between hover:bg-lighter p-3 border-t border-lighter focus:outline-none">
        <div>
          <p class="text-sm text-left leading-tight text-dark pb-1">{{ trend.top }}</p>
          <p class="font-bold text-left leading-tight pb-2">#{{ trend.title }}</p>
          <p class="text-sm text-left leading-tight text-dark">{{ trend.bottom }}</p>
        </div>
        <i class="fas fa-angle-down text-lg font-semibold text-dark"></i>
      </button>
      <button class="p-3 w-full hover:bg-lighter text-left text-blue border-t border-lighter focus:outline-none">
        Show more
      </button>
    </div>
    <div class="w-full rounded-lg bg-lightest mt-6">
      <div class="px-3 py-2">
        <p class="text-xl font-extrabold">Who to follow</p>
      </div>
      <button v-for="friend in friends" :key="friend.handle" class="w-full flex items-center hover:bg-lighter p-3 border-t border-lighter focus:outline-none">
        <img :src="friend.src" :name="friend.name" :alt="friend.name" class="w-12 h-12 rounded-full"> 
        <div class="ml-4">
          <p class="text-sm font-bold leading-tight text-left pb-1"> {{ friend.name }} </p>
          <p class="text-sm leading-tight text-dark text-left"> {{ friend.handle }} </p>
        </div>
        <button class="ml-auto text-sm text-blue py-1 px-4 rounded-full border-2 border-blue">Follow</button>
      </button>
      <button class="p-3 w-full hover:bg-lighter text-left text-blue border-t border-lighter">
        Show more
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Trendings',
    data() {
      return {
        trending: [
          {top: 'Trending in TX', title: 'Gigi', bottom: 'Trending with: Rip Gigi'},
          {top: 'Music', title: 'WeWon', bottom: '135K Tweets'},
          {top: 'Pop', title: 'BlueIvy', bottom: '40k tweets'},
          {top: 'Trending in US', title: 'DenimDay', bottom: '40k tweets'},
          {top: 'Trending', title: 'WhenBeyonce', bottom: '25.4k tweets'},
        ],
        friends: [
          {src: require('../assets/images/elonmusk.jpg'), name: 'Elon Musk', handle: '@teslaBoy'},
          {src: require('../assets/images/ronaldo.jpg'), name: 'Cristiano Ronaldo', handle: '@Cristiano'},
          {src: require('../assets/images/marshmello.jpg'), name: 'Marshmello', handle: '@marshmellomusic'}
        ],
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>