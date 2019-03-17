<template>
  <li>
    <h2>
      <a :href="artist.url" target="_blank">{{artist.name}}
        <img :src="artist.image[2]['#text']" alt="">
      </a>
    </h2>
  </li>
</template>

<script>
  export default {
    name: 'artist',
    props: ['artist'],
    data() {
      return {
        artists: []
      }
    }
  }
</script>

<style lang="stylus" scoped>
li.artist
  display block
  margin 10px 0
</style>
