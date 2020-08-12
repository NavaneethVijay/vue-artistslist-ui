<template>
  <div class="h-screen">
    <div class="max-w-sm mx-auto">
      <div class="py-4 px-2 flex flex-row items-center justify-between">
      <div
        class="tracking-widest flex text-purple-600 font-medium items-center rounded-lg focus:outline-none focus:shadow-outline"
      >
      <svg viewBox="0 0 20 20" fill="currentColor" class="w-8 h-8 text-purple-600 mr-1"
          width="54"><path fill-rule="evenodd" d="M9.504 1.132a1 1 0 01.992 0l1.75 1a1 1 0 11-.992 1.736L10 3.152l-1.254.716a1 1 0 11-.992-1.736l1.75-1zM5.618 4.504a1 1 0 01-.372 1.364L5.016 6l.23.132a1 1 0 11-.992 1.736L4 7.723V8a1 1 0 01-2 0V6a.996.996 0 01.52-.878l1.734-.99a1 1 0 011.364.372zm8.764 0a1 1 0 011.364-.372l1.733.99A1.002 1.002 0 0118 6v2a1 1 0 11-2 0v-.277l-.254.145a1 1 0 11-.992-1.736l.23-.132-.23-.132a1 1 0 01-.372-1.364zm-7 4a1 1 0 011.364-.372L10 8.848l1.254-.716a1 1 0 11.992 1.736L11 10.58V12a1 1 0 11-2 0v-1.42l-1.246-.712a1 1 0 01-.372-1.364zM3 11a1 1 0 011 1v1.42l1.246.712a1 1 0 11-.992 1.736l-1.75-1A1 1 0 012 14v-2a1 1 0 011-1zm14 0a1 1 0 011 1v2a1 1 0 01-.504.868l-1.75 1a1 1 0 11-.992-1.736L16 13.42V12a1 1 0 011-1zm-9.618 5.504a1 1 0 011.364-.372l.254.145V16a1 1 0 112 0v.277l.254-.145a1 1 0 11.992 1.736l-1.735.992a.995.995 0 01-1.022 0l-1.735-.992a1 1 0 01-.372-1.364z" clip-rule="evenodd"></path></svg>
          Patlify
      </div>
    
    </div>
      <div class="pb-4 px-2">
        <h1 class="font-bold text-4xl">Hi! Navaneeth.</h1>
        <h1 class="font-medium text-2xl">Artists you follow</h1>
      </div>
      <div class="w-full sticky top-0 py-4 bg-purple-100 rounded">
        <ul class="flex flex-no-wrap overflow-x-scroll pillmain">
          <li
            @click="scrollTo(index)"
            v-for="(artist, index) in artistsList"
            :key="index"
            :class="`bg-${colors[index]}-600`"
            class="m-1 rounded-full flex items-center justify-center text-white tabpill overflow-hidden"
          >
            <div class="flex flex-no-wrap w-full items-center justify-start pillcontent">
              <img :src="artist.images[2].url" class="rounded-full w-5 h-5" />
              <div class="text-md font-medium mr-2 pilltitle">{{ artist.name }}</div>
            </div>
          </li>
        </ul>
      </div>
      <div class="px-2 md:px-0">
        <ScrollListItem
          :id="`appDetail${index}`"
          :artist="{ 
            id: artist.id,
            color: colors[index],
            name: artist.name,
            image: artist.images[0].url,
            about: artistAbout[index],
            albums: artist.albums
          }"
          v-for="(artist, index) in artistsList"
          :key="index"
        />
      </div>
    </div>
  </div>
</template>
<script>
import VirtualList from 'vue-virtual-scroll-list'
import artistsData from '@/api/artists'
export default {
  components: {
    VirtualList,
  },
  data() {
    return {
      artistsList: [],
      artistIds: [
        '06HL4z0CvFAxyc27GXpf02',
        '69GGBxA162lTqCwzJG5jLp',
        '5Pwc4xIPtQLFEnJriah9YJ',
        '66CXWjxzNUsdJxJ2JdwvnR',
        '4rTv3Ejc7hKMtmoBOK1B4T',
        '6M2wZ9GZgrQXHCFfjv46we',
        '4gzpq5DPGxSnKTe4SA8HAU',
        '540vIaP2JwjQb9dm3aArA4',
      ],
      artistAbout: [
        'Taylor Alison Swift is an American singer-songwriter. Her narrative songwriting, which often centers around her personal life, has received widespread media coverage.',
        'The Chainsmokers is an American electronic DJ and production duo consisting of Alexander "Alex" Pall and Andrew "Drew" Taggart. They started out by releasing remixes of songs by indie artists.',
        'OneRepublic is an American alternative rock band formed in Colorado Springs, Colorado, in 2002. It consists of lead vocalist and multi-instrumentalist Ryan Tedder, guitarist Zach Filkins, guitarist Drew Brown, bassist and cellist Brent Kutzle, drummer Eddie Fisher and keyboardist Brian Willett.',
        'Ariana Grande-Butera is an American singer, songwriter, and actress. Born in Boca Raton, Florida, Grande began her career in the 2008 Broadway musical 13.',
        'Ali Gatie is an Iraqi–Canadian rapper, singer and songwriter. His 2019 song "Its You" charted worldwide, charting on the US Billboard Hot 100 and reaching the top 40 in Australia, Canada, Ireland and Sweden and the top 10 in New Zealand and in Germany.',
        'Dua Lipa is an English singer and songwriter. After working as a model, she signed with Warner Music Group in 2015 and released her self-titled debut album in 2017.',
        'Coldplay are a British rock band that were formed in London in 1996. Vocalist and pianist Chris Martin, guitarist Jonny Buckland, bassist Guy Berryman, and drummer Will Champion met at University College...',
        'William Sami Étienne Grigahcine, better known by his stage name DJ Snake, is a French DJ and record producer from Paris, France. He made his international debut with singles "Bird Machine" and "Turn Down for What" in 2013',
      ],
      colors: [
        'pink',
        'yellow',
        'blue',
        'green',
        'purple',
        'teal',
        'red',
        'gray',
      ],
    }
  },

  mounted() {
    this.artistsList = artistsData
  },
  methods: {
    // async fetchSomething() {
    //   this.$axios.setToken(
    //     'BQBLzCT_s2d9PDrbfisrKGtb7KZrhWZgg7hD_5S2ly4LrAtJRrDrBYW_-luMknQ00zcu_ibIqO1g_e61Mt7Z2WCVPGlftJYyH5wqQfhEujLNPwQLvS__hUR9LL1As_nJtxMJKegiRqp8mGe5ZarAX7WqtqMNmno',
    //     'Bearer'
    //   )
    //   const { artists } = await this.$axios.$get(
    //     `https://api.spotify.com/v1/artists?ids=${this.artistIds.toString()}`
    //   )
    //   artists.map((artist) => {
    //     let { id, name, genres, images, href } = artist
    //     this.artistsList.push({ id, name, genres, images, href })
    //   })
    // },
    scrollTo(index) {
      document.getElementById(`appDetail${index}`).scrollIntoView({
        behavior: 'smooth',
        block: 'start',
      })
    },
  },
}
</script>
<style lang="scss">
.items-details-main {
  max-height: 100vh;
}
.pillmain::-webkit-scrollbar {
  display: none;
}
.tabpill {
  min-width: 3.2rem;
  min-height: 3.2rem;
  transition: all 0.8s cubic-bezier(0.19, 1, 0.22, 1);
  img {
    min-width: 2.6rem;
    min-height: 2.6rem;
    transform: translateX(4.5px);
  }
  .pillcontent {
    .pilltitle {
      min-width: max-content;
      transform: translateX(30px);
      opacity: 0;
      transition: all 0.4s ease-in-out;
    }
  }
  &:hover {
    justify-content: flex-start;
    overflow: visible;
    min-width: 160px;
    .pilltitle {
      opacity: 1;
      transform: translateX(10px);
    }
  }
}
</style>