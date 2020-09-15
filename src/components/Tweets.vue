<template>
  <div class="w-1/2 h-full overflow-y-scroll">
    <div class="px-5 py-3 border-b border-lighter flex justify-between items-center">
      <h1 class="text-xl font-extrabold">Home</h1>
      <i class="far fa-star text-blue text-xl"></i>
    </div>
    <div class="px-5 py-3 border-b-8 border-lighter flex">
      <div class="flex-none">
        <img src="../assets/images/pp.jpg" alt="pp" class="flex-none w-12 h-12 rounded-full">
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
          <img src="../assets/images/pp.jpg" class="h-12 w-12 rounded-full flex-none"/>
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
    <div v-for="follow in following" :key="follow.tweet" class="w-full p-4 flex border-b hover:bg-lightest">
      <div class="flex-none mr-4">
        <img :src="follow.src" :alt="follow.name" class="w-12 h-12 rounded-full flex-none">
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
</template>

<script>
export default {
  name: 'Tweets',
  data() {
    return {
      following: [
        {src: require('../assets/images/elonmusk.jpg'), name: 'Elon Musk', handle: '@teslaBoy', time: '20 min', tweet: 'Should I just quarantine on mars??', comments: '11,835', retweets: '5560', likes: '190,003'},
        {src: require('../assets/images/marshmello.jpg'), name: 'Marshmello', handle: '@marshmellomusic', time: '55 min', tweet: 'New music is coming!!!', comments: '2,030', retweets: '500', likes: '20,003'},
        {src: require('../assets/images/ronaldo.jpg'), name: 'Cristiano Ronaldo', handle: '@Cristiano', time: '2 hr', tweet: 'I hurt my leg today :(', comments: '2365', retweets: '4965', likes: '40,003'},
        {src: require('../assets/images/elonmusk.jpg'), name: 'Elon Musk', handle: '@teslaBoy', time: '3 hr', tweet: 'Just did something crazyyyyyyy', comments: '10,500', retweets: '54,252', likes: '276,103'}
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