<template>
  <div class="about">
    <cropper :isShowCropper="true" ></cropper>
  </div>  
</template>
<script>
import cropper from "../components/cropper.vue"
export default {
  name:'about',
  components: {
    cropper
  },
  data() {
    return {
    }
 },
  computed: {},
  created() {},
  mounted() {},
  methods: {},
};
</script>

<style scoped lang="scss">

</style>
