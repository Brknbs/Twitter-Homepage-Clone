<template>
  <div id="app" class="flex container h-screen w-full">
    <div class="lg:w-1/5 border-r border-lighter px-2 lg:px-6 py-2 flex flex-col justify-between">
      <div>
        <button class="h-12 w-12 hover:bg-lightblue text-3xl rounded-full text-blue mb-3 focus:outline-none">
          <i class="fab fa-twitter"></i>
        </button>
        <div>
          <button @click="id = tab.id" v-for="tab in tabs" :key="tab.id" :class="`flex items-center py-2 px-4 hover:bg-lightblue rounded-full mr-auto hover:text-blue mb-3 focus:outline-none ${id === tab.id ? 'text-blue' : ''}`">
            <i :class="`${tab.icon} text-2xl mr-5 text-left `"></i>
            <p class="text-lg font-bold text-left hidden lg:block">{{ tab.title }}</p>
          </button>
        </div>
        <button class="text-white bg-blue rounded-full font-semibold w-12 h-12 lg:h-auto lg:w-full p-3 focus:outline-none hover:bg-darkblue">
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
      dropdown: false
    }
  }
}
</script>

<style lang="scss">

</style>
