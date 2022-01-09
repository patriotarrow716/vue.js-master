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
      trending: [
        { top: 'Trending in TX', title: 'Gigi', bottom: 'Trending with: Rip Gigi' },
        { top: 'Music', title: 'We Won', bottom: '135K Tweets' },
        { top: 'Pop', title: 'Blue Ivy', bottom: '40k tweets' },
        { top: 'Trending in US', title: 'Denim Day', bottom: '40k tweets' },
        { top: 'Trending', title: 'When Beyonce', bottom: '25.4k tweets' },
      ],
      friends: [
        { src: 'man.jpg', name: 'male', handle: '@male' },
        { src: 'woman.jpg', name: 'woman', handle: '@woman' },
        { src: 'bmw.jpg', name: 'bmwJapan', handle: '@bmw.jp' }
      ],
      following: [
        { src: 'man.jpg', name: 'male', handle: '@male', time: '20 min', tweet: 'Should I just quarantine on mars??', comments: '1,000', retweets: '550', like: '1,000,003' },
        { src: 'woman.jpg', name: 'woman', handle: '@woman', time: '55 min', tweet: 'Should me and the rock do another sub-par movie together????', comments: '2,030', retweets: '50', like: '20,003' },
        { src: 'man.jpg', name: 'male', handle: '@male', time: '1.4 hr', tweet: 'Haha just made a flame thrower. Shld I sell them?', comments: '100,000', retweets: '1,000,002', like: '5,000,003' },
        { src: 'man.jpg', name: 'male', handle: '@male', time: '1.4 hr', tweet: 'Just did something crazyyyyyyy', comments: '100,500', retweets: '1,000,032', like: '5,000,103' }
      ],
    }
  }
}
</script>


<template>
  <div id="app" class="flex container h-screen w-full">
    <!-- サイドナビ　セクション -->
    <div class="lg:w-1/5 border-r border-lighter lpx-2 lg:px-6 py-2 flex flex-col justify-between">
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
          class="text-white bg-blue rounded-full font-semibold focus:outline-none lg:h-auto lg:w-full w-full p-3 hover:bg-darkblue"
        >
          <p class="hidden lg:block">ツイートする</p>
          <i class="fas fa-plus lg:hidden"></i>
        </button>
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

          <i class="hidden lg:block fas fa-ellipsis-h ml-auto text-lg"></i>
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

    <!-- ツイートセクション -->
    <div class="w-full md:w-1/2 h-full overflow-y-scroll">
      <div class="px-5 py-3 border-b border-lighter flex items-center justify-between">
        <h1 class="text-xl font-bold">ホーム</h1>
        <i class="far fa-star text-xl text-black"></i>
      </div>
      <div class="px-5 py-3 border-b-8 border-lighter flex">
        <div class="flex-none">
          <img
            src="https://images.unsplash.com/photo-1561047029-196d190f0713?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=387&q=80"
            class="flex-none w-12 h-12 rounded-full border border-lighter"
            alt
          />
        </div>
        <form class="w-full px-4 relative border-transparent">
          <textarea
            placeholder="今どうしてる？"
            class="mt-3 pb-3 w-full focus:outline-none border-transparent hover:border-white"
          />
          <div class="flex items-center">
            <i class="text-lg text-blue mr-4 far fa-image"></i>
            <i class="text-lg text-blue mr-4 fas fa-film"></i>
            <i class="text-lg text-blue mr-4 far fa-chart-bar"></i>
            <i class="text-lg text-blue mr-4 far fa-smile"></i>
          </div>
          <button
            type="submit"
            class="h-10 px-4 text-white font-semibold bg-blue hover:bg-darkblue focus:outline-none rounded-full absolute bottom-0 right-0"
          >ツイートする</button>
        </form>
      </div>
      <div v-for="follow in following" class="w-full p-4 border-b hover:bg-lighter flex">
        <div class="flex-none mr-4">
          <img :src="`${follow.src}`" class="h-12 w-12 rounded-full flex-none" />
        </div>
        <div class="w-full">
          <div class="flex items-center w-full">
            <p class="font-semibold">{{ follow.name }}</p>
            <p class="text-sm text-dark ml-2">{{ follow.handle }}</p>
            <p class="text-sm text-dark ml-2">{{ follow.time }}</p>
            <i class="fas fa-angle-down text-lg text-dark ml-auto"></i>
          </div>
          <p class="py-2">{{ follow.tweet }}</p>
          <div class="flex items-center justify-between w-full">
            <div class="flex items-center text-sm text-dark">
              <i class="far fa-comment mr-3"></i>
              <p>{{ follow.components }}</p>
            </div>

            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-retweet mr-3"></i>
              <p>{{ follow.retweets }}</p>
            </div>
            <!-- <div class="flex items-center justify-between w-full"> -->
            <div class="flex items-center text-sm text-dark">
              <i class="far fa-heart mr-3"></i>
              <p>{{ follow.like }}</p>
            </div>
            <!-- </div> -->
            <!-- <div class="flex items-center justify-between w-full"> -->
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-share-square"></i>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- トレンドセクション -->
    <div
      class="md:block hidden w-1/3 h-full border-l border-lighter py-2 px-6 overflow-y-scroll relative"
    >
      <input class="pl-12 rounded-full w-full p-2 bg-lighter text-sm" placeholder="キーワード検索" />
      <i class="fas fa-search absolute left-0 top-0 mt-5 ml-12 text-sm text-light"></i>
      <div class="w-full rounded-lg bg-lightest">
        <div class="flex items-center justify-between p-3">
          <p class="text-lg font-bold">いまどうしてる？</p>
          <i class="fas fa-cog text-lg text-blue"></i>
        </div>
        <button
          v-for="trend in trending"
          class="w-full flex justify-between hover:bg-lighter p-3 border-t border-lighter"
        >
          <div>
            <p class="text-sm text-left leading-tight text-dark">{{ trend.top }}</p>
            <p class="font-bold text-left leading-tight">{{ trend.title }}</p>
            <p class="text-left leading-tight text-dark">{{ trend.bottom }}</p>
          </div>
          <i class="fas fa-angle-down text-lg text-dark"></i>
        </button>
        <button
          class="p-3 w-full hover:bg-lighter text-left text-blue border-r border-lighter"
        >さらに表示</button>
      </div>
      <div class="w-full rounded-lg bg-lightest my-4">
        <div class="p-3">
          <p class="text-lg font-bold">おすすめユーザー</p>
        </div>
        <button
          v-for="friend in friends"
          class="w-full flex hover:bg-lighter p-3 border-t border-lighter"
        >
          <img :src="`${friend.src}`" class="w-12 h-12 rounded-full border border-lighter" />

          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight">{{ friend.name }}</p>
            <p class="text-sm leading-tight">{{ friend.handle }}</p>
          </div>
          <button
            class="ml-auto text-sm text-white bg-black py-1 px-4 rounded-full border-2 border-black"
          >フォロー</button>
        </button>
        <button
          class="p-3 w-full hover:bg-lighter text-left text-blue border-r border-lighter"
        >さらに表示</button>
      </div>
    </div>
  </div>
</template>





