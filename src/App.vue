<script>
export default {
  name: 'app',
  components: {
  },
  data() {
    return {
      tabs: [
        { icon: 'fas fa-home', title: 'ホーム', id: 'home' },
        { icon: 'fas fa-hashtag', title: '話題を検索', id: 'explore' },
        { icon: 'far fa-bell', title: '通知', id: 'notifications' },
        { icon: 'far fa-envelope', title: 'メッセージ', id: 'messages' },
        { icon: 'far fa-bookmark', title: 'ブックマーク', id: 'bookmarks' },
        { icon: 'fas fa-clipboard-list', title: 'リスト', id: 'lists' },
        { icon: 'far fa-user', title: 'プロフィール', id: 'profile' },
        { icon: 'fas fa-ellipsis-h', title: 'もっと見る', id: 'more' },
      ],
      id: 'home',
      dropdown: false,
    }
  }
}
</script>


<template>
  <div id="app" class="flex container h-screen w-full">
    <!-- サイドナビ -->
    <div class="lg:w-1/5 border-r border-lighter px-8 py-2 flex flex-col justify-between">
      <div>
        <button class="h-12 w-12 hover:bg-lightblue text-3xl rounded-full text-blue">
          <i class="fab fa-twitter"></i>
        </button>
        <div>
          <button
            v-for="tab in tabs"
            @click="id = tab.id"
            :class="`focus:outline-none hover:text-blue flex items-center py-2 px-4 hover:bg-lightblue rounded-full mr-auto mb-3 ${id === tab.id ? 'text-blue' : ''}`"
          >
            <i :class="`${tab.icon} text-2xl mr-4 text-left`"></i>
            <p class="text-lg font-semibold text-left hidden lg:block">{{ tab.title }}</p>
          </button>
        </div>
        <button
          class="text-white bg-blue rounded-full font-semibold focus:outline-none w-full p-3 hover:bg-darkblue"
        >ツイートする</button>
      </div>
      <div class="lg:w-full relative">
        <button
          @click="dropdown = true"
          class="flex items-center w-full hover:bg-lightblue rounded-full p-2 focus:outline-none"
        >
          <img
            src="https://images.unsplash.com/photo-1561047029-196d190f0713?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=387&q=80"
            class="w-10 h-10 rounded-full border border-lighter"
          />
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight">coffee</p>
            <p class="text-sm leading-tight">@I like coffee</p>
          </div>
          <i class="hidden lg:block fas fa-angle-down ml-auto text-lg"></i>
        </button>

        <div
          v-if="dropdown === true"
          class="absolute bottom-0 left-0 w-64 rounded-lg shadow-md border-lightest bg-white mb-16"
        >
          <button
            @click="dropdown = false"
            class="p-3 flex items-center w-full hover:bg-lightest p-2 focus:outline-none"
          >
            <img
              src="https://images.unsplash.com/photo-1561047029-196d190f0713?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=387&q=80"
              class="w-10 h-10 rounded-full border border-lighter"
            />
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight">cafe</p>
              <p class="text-sm leading-tight">@I like coffee</p>
            </div>
            <i class="fas fa-check ml-auto text-blue"></i>
          </button>
          <button
            @click="dropdown = false"
            class="w-full text-left hover:bg-lightest border-r border-lighter p-3 test-sm"
          >Add an existing account</button>
          <button
            @click="dropdown = false"
            class="w-full text-left hover:bg-lightest border-r border-lighter p-3 test-sm"
          >Log out @I like coffee</button>
        </div>
      </div>
    </div>
  </div>
</template>





