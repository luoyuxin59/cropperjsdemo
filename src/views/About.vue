<template>
  <div class="about">
    <vuecropper :isShowCropper="true" ></vuecropper>
  </div>  
</template>
<script>
import vuecropper from "../components/common/vuecropper.vue"
export default {
  name:'about',
  components: {
    vuecropper
  },
  data() {
    return {}
 },
  computed: {},
  created() {},
  mounted() {},
  methods:  {},
};
</script>

<style scoped lang="scss">

</style>
