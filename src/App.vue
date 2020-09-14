<template>
  <div id="app" class="flex container h-screen w-full">
    <!-- navbar -->
    <div class="lg:w-1/5 border-r border-lighter px-2 lg:px-6 py-2 flex flex-col justify-between">
      <div>
        <button class="h-12 w-12 hover:bg-lightblue text-3xl rounded-full text-blue mb-3 ml-1 focus:outline-none">
          <i class="fab fa-twitter"></i>
        </button>
        <div>
          <button @click="id = tab.id" v-for="tab in tabs" :key="tab.id" :class="`flex items-center py-2 px-4 hover:bg-lightblue rounded-full mr-auto hover:text-blue mb-3 focus:outline-none ${id === tab.id ? 'text-blue' : ''}`">
            <i :class="`${tab.icon} text-2xl mr-5 text-left `"></i>
            <p class="text-lg font-bold text-left hidden lg:block">{{ tab.title }}</p>
          </button>
        </div>
        <button class="text-white bg-blue rounded-full font-semibold w-12 h-12 lg:h-auto lg:w-full p-3 focus:outline-none hover:bg-darkblue mb-3">
          <p class="hidden lg:block">Tweet</p>
          <i class="fas fa-plus lg:hidden"></i>
        </button>
      </div>
      <div class="lg:w-full relative">
        <button class="flex items-center w-full focus:outline-none hover:bg-lightblue rounded-full p-2" @click="dropdown = !dropdown"> 
          <img src="./assets/images/pp.jpg" alt="pp" class="w-10 h-10 rounded-full"> 
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight"> Berkan </p>
            <p class="text-sm leading-tight text-light"> @Brknbs </p>
          </div>
          <i class="fas fa-angle-down ml-auto text-lg hidden lg:block"></i>
        </button>
        <div v-if="dropdown" class="absolute bottom-0 right-0 w-64 rounded-lg shadow-md border-lightest bg-white mb-16">
          <button class="flex items-center w-full focus:outline-none hover:bg-lightest p-4" @click="dropdown = false">
            <img src="./assets/images/pp.jpg" alt="pp" class="w-10 h-10 rounded-full"> 
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight"> Berkan </p>
              <p class="text-sm leading-tight text-light"> @Brknbs </p>
            </div>
            <i class="fas fa-check ml-auto text-blue"></i>
          </button>
          <button class="w-full text-left hover:bg-lightest border-t border-lighter p-4 text-sm focus:outline-none" @click="dropdown = false">
            Add an existing account
          </button>
          <button class="w-full text-left hover:bg-lightest border-t border-lighter p-4 text-sm focus:outline-none" @click="dropdown = false">
            Log out @Brknbs
          </button>
        </div>
      </div>
    </div>

    <!-- tweets -->
    <div class="w-1/2 h-full overflow-y-scroll">
      <div class="px-5 py-3 border-b border-lighter flex justify-between items-center">
        <h1 class="text-xl font-extrabold">Home</h1>
        <i class="far fa-star text-blue text-xl"></i>
      </div>
      <div class="px-5 py-3 border-b-8 border-lighter flex">
        <div class="flex-none">
          <img src="./assets/images/pp.jpg" alt="pp" class="flex-none w-12 h-12 rounded-full">
        </div>
        <form @submit.prevent="addNewTweet" class="w-full px-4 relative">
          <textarea v-model="tweet.content" placeholder="What's up?" class="focus:outline-none w-full mt-3 pb-3"></textarea>
          <div class="flex items-center">
            <i class="text-xl text-blue mr-4 far fa-image cursor-pointer"></i>
            <i class="text-xl text-blue mr-4 fas fa-film cursor-pointer"></i>
            <i class="text-xl text-blue mr-4 far fa-chart-bar cursor-pointer"></i>
            <i class="text-xl text-blue mr-4 far fa-smile cursor-pointer"></i>
          </div>
          <button type="submit" class="h-10 px-4 text-white font-semibold bg-blue hover:bg-darkblue rounded-full focus:outline-none absolute bottom-0 right-0">Tweet</button>
        </form>
      </div>
      <div class="flex flex-col-reverse">
        <div v-for="tweet in tweets" :key="tweet.content" class="w-full p-4 border-b hover:bg-lighter flex">
          <div class="flex-none mr-4">
            <img src="./assets/images/pp.jpg" class="h-12 w-12 rounded-full flex-none"/>
          </div>
          <div class="w-full">
            <div class="flex items-center w-full">
              <p class="font-semibold"> Berkan </p>
              <p class="text-sm text-dark ml-2"> @Brknbs </p>
              <p class="text-sm text-dark ml-2"> 1 sec </p>
              <i class="fas fa-angle-down text-dark ml-auto"></i>
            </div>
            <p class="pb-2">
              {{ tweet.content }}
            </p>
            <div class="flex items-center justify-between w-full">
              <div class="flex items-center text-sm text-dark">
                <i class="far fa-comment mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-retweet mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="far fa-heart mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-external-link-alt mr-3"></i>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div v-for="follow in following" :key="follow.handle" class="w-full p-4 flex border-b hover:bg-lightest">
        <div class="flex-none mr-4">
          <img :src="require(`${follow.src}`)" :alt="follow.name" class="w-12 h-12 rounded-full flex-none">
        </div>
        <div class="w-full">
          <div class="flex items-center w-full">
            <p class="font-bold">{{ follow.name }}</p>
            <p class="text-sm text-dark ml-2">{{ follow.handle }}</p>
            <p class="ml-2 text-sm text-dark">&middot;</p>
            <p class="text-sm text-dark ml-2">{{ follow.time }}</p>
            <i class="fas fa-angle-down text-dark ml-auto"></i>
          </div>
          <p class="pb-2">{{ follow.tweet }}</p>
          <div class="w-full flex items-center justify-between">
            <div class="flex items-center text-sm text-dark">
              <i class="far fa-comment mr-3"></i>
              <p>{{ follow.comments }}</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-retweet mr-3"></i>
              <p>{{ follow.retweets }}</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="far fa-heart mr-3"></i>
              <p>{{ follow.likes }}</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-external-link-alt mr-3"></i>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- trendings -->
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
          <img :src="require(`${friend.src}`)" :name="friend.name" :alt="friend.name" class="w-12 h-12 rounded-full"> 
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
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      tabs: [
        {icon: 'fas fa-home', title: 'Home', id:'home'},
        {icon: 'fas fa-hashtag', title: 'Explore', id: 'explore'},
        {icon: 'far fa-bell', title: 'Notifications', id: 'notifications'},
        {icon: 'far fa-envelope', title: 'Messages', id: 'messages'},
        {icon: 'far fa-bookmark', title: 'Bookmarks', id: 'bookmarks'},
        {icon: 'fas fa-clipboard-list', title: 'Lists', id: 'lists'},
        {icon: 'far fa-user', title: 'Profile', id: 'profile'},
        {icon: 'fas fa-ellipsis-h', title: 'More', id: 'more'}
      ],
      id: '',
      dropdown: false,
      trending: [
        {top: 'Trending in TX', title: 'Gigi', bottom: 'Trending with: Rip Gigi'},
        {top: 'Music', title: 'WeWon', bottom: '135K Tweets'},
        {top: 'Pop', title: 'BlueIvy', bottom: '40k tweets'},
        {top: 'Trending in US', title: 'DenimDay', bottom: '40k tweets'},
        {top: 'Trending', title: 'WhenBeyonce', bottom: '25.4k tweets'},
      ],
      friends: [
        {src: './assets/images/elonmusk.jpg', name: 'Elon Musk', handle: '@teslaBoy'},
        {src: './assets/images/ronaldo.jpg', name: 'Cristiano Ronaldo', handle: '@Cristiano'},
        {src: './assets/images/marshmello.jpg', name: 'Marshmello', handle: '@marshmellomusic'}
      ],
      following: [
        {src: './assets/images/elonmusk.jpg', name: 'Elon Musk', handle: '@teslaBoy', time: '20 min', tweet: 'Should I just quarantine on mars??', comments: '11,835', retweets: '5560', likes: '190,003'},
        {src: './assets/images/marshmello.jpg', name: 'Marshmello', handle: '@marshmellomusic', time: '55 min', tweet: 'New music is coming!!!', comments: '2,030', retweets: '500', likes: '20,003'},
        {src: './assets/images/ronaldo.jpg', name: 'Cristiano Ronaldo', handle: '@Cristiano', time: '2 hr', tweet: 'I hurt my leg today :(', comments: '2365', retweets: '4965', likes: '40,003'},
        {src: './assets/images/elonmusk.jpg', name: 'Elon Musk', handle: '@teslaBoy', time: '3 hr', tweet: 'Just did something crazyyyyyyy', comments: '10,500', retweets: '54,252', likes: '276,103'}
      ],
      tweets: [],
      tweet: {content: ''}
    }
  },
  methods: {
    addNewTweet() {
      let newTweet = {
        content: this.tweet.content
      };
      this.tweets.push(newTweet);
    }
  }
}
</script>

<style lang="scss">

</style>
