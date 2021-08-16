<template>
  <div id="app">
    <div id="nav">
      <!-- <router-link to="/">Cropper</router-link> |
      <router-link to="/about">vue-Cropper</router-link> |
      <router-link to="/uedit">ueditor</router-link> -->
      <home-nav></home-nav>
    </div>
    <router-view/>
  </div>
</template>

<script>
import HomeNav from './components/comoent/HomeNav.vue'
export default {
  components: {
    HomeNav
  },

}
</script>
<style lang="scss">

</style>
