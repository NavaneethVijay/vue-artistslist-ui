<template>
  <div class="mb-6 mt-2 shadow-xl rounded-lg">
    <div
      :class="`bg-${artist.color}-100 pl-2 pr-6 py-4 rounded-t-lg flex justify-between items-center`"
    >
      <div :class="`text-${artist.color}-700 flex items-center`">
        <img :src="artist.image ? artist.image : ''" class="rounded-full w-8 h-8" />
        <h3 class="font-medium ml-2 text-lg">{{ artist.name }}</h3>
      </div>
      <div>
        <svg viewBox="0 0 20 20" fill="currentColor" class="inline-block check w-6 h-6">
          <path
            fill-rule="evenodd"
            d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
            clip-rule="evenodd"
          />
        </svg>
        <span class="text-sm">Following</span>
      </div>
    </div>
    <div class="bg-white py-4 rounded-lg overflow-hidden">
      <div class="info-card px-4 pt-4">
        <img :src="artist.image ? artist.image : ''" class="rounded-full shadow-xl w-40 h-40" />
        <h3 class="font-bold text-3xl mt-4">{{ artist.name }}</h3>
        <p class="text-sm text-gray-600">{{ artist.about }}</p>
      </div>
      <table class="w-full mt-4">
        <thead>
          <tr>
            <th
              class="px-4 py-3 border-b border-gray-200 bg-gray-50 text-left text-base leading-4 font-medium text-gray-500 uppercase tracking-wider"
            >Popular Albums</th>
          </tr>
        </thead>
        <tbody class="bg-white divide-y divide-gray-200">
          <tr v-for="(album, index) in artist.albums" :key="index">
            <td class="px-4 py-4 whitespace-no-wrap border-b border-gray-200">
              <div class="flex items-center">
                <div class="flex-shrink-0 h-10 w-10">
                  <img class="h-10 w-10 rounded-full shadow-xl" :src="album.images[1].url" alt />
                </div>
                <div class="ml-4 w-9/12">
                  <p class="text-sm leading-5 truncate w-full block font-medium text-gray-900 capitalize">{{ album.name }}</p>
                  <div class="text-sm leading-5 text-gray-500">{{ new Date(album.release_date).toDateString() }}</div>
                </div>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  name: 'ScrollListItem',
  data() {
    return {
      albums: [],
    }
  },
  props: {
    artist: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  // async mounted() {
  //   this.getArtistAlbums()
  // },
  // methods: {
  //   async getArtistAlbums() {
  //     this.$axios.setToken(
  //       'BQBLzCT_s2d9PDrbfisrKGtb7KZrhWZgg7hD_5S2ly4LrAtJRrDrBYW_-luMknQ00zcu_ibIqO1g_e61Mt7Z2WCVPGlftJYyH5wqQfhEujLNPwQLvS__hUR9LL1As_nJtxMJKegiRqp8mGe5ZarAX7WqtqMNmno',
  //       'Bearer'
  //     )
  //     const { items } = await this.$axios.$get(
  //       `https://api.spotify.com/v1/artists/${this.artist.id}/albums?market=ES&limit=4`
  //     )
  //     this.albums = items
  //   },
  // },
}
</script>