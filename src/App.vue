<template>
  <div id="app">
    <img src="https://dardels3.github.io/platzi-music/dist/logo.png">
    <h1>Plazi Music</h1>
    <select v-model="selectedCountry" class="" name="">
      <option v-for="country in countries" :value="country.value">{{country.name}}</option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <artist v-for="artist in artists" :key="artist.mbid" :artist="artist"></artist>
    </ul>
  </div>
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { name: 'Argentina', value: 'argentina'},
        { name: 'Brazil', value: 'brazil'},
        { name: 'Perú', value: 'peru'}
      ],
      selectedCountry: 'argentina',
      loading: true
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtist() {
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
      .then(function (artists) {
        self.loading = false
        self.artists = artists
      })
    }
  },
  mounted() {

  },
  watch: {
    selectedCountry: function () {
      this.refreshArtist()
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
	list-style-type none
	padding 0
li
	display inline-block
	margin 0 10px
a
	color #42b983
</style>
