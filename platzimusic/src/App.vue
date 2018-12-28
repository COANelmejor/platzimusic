<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 PlatziMusic
    select(v-model="selectedcountry")
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" :key="artist.mbid")
</template>

<script>
import getArtists from './api/index'
import Artist from './components/Artist.vue'
export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [{
        name: 'Argentina',
        value: 'argentina'
      },{
        name: 'Guatemala',
        value: 'guatemala'
      },{
        name: 'Japón',
        value: 'japan'
      }],
      selectedcountry: 'japan'
    }
  },
  components: {
    Artist
  },
  methods:{
    refreshArtists() {
      const self = this;
      console.log(self);
      getArtists(this.selectedcountry)
      .then(function (artists) {
        console.log(artists);
        self.artists = artists
      })
    }
  },
  mounted() {
    this.refreshArtists()
  },
  watch: {
    selectedcountry () {
      this.refreshArtists()
    }
  }
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px

h1, h2
  font-weight normal

ul
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983
</style>
