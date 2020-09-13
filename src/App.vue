<template>
  <div id="app" class="flex container h-screen w-full">
    <div class="w-1/5 border-r border-lighter px-8 py-2">
      <button class="h-12 w-12 hover:bg-lightblue text-3xl rounded-full text-blue mb-3">
        <i class="fab fa-twitter"></i>
      </button>
      <div>
        <button @click="id = tab.id" v-for="tab in tabs" :key="tab.id" :class="`flex items-center py-2 px-4 hover:bg-lightblue rounded-full mr-auto hover:text-blue mb-3 focus:outline-none ${id === tab.id ? 'text-blue' : ''}`">
          <i :class="`${tab.icon} text-2xl mr-4 text-left`"></i>
          <p class="text-lg font-bold text-left">{{ tab.title }}</p>
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
      id: ''
    }
  }
}
</script>

<style lang="scss">

</style>
