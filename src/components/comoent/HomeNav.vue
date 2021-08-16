<template>
  <div class="">
    <el-menu
      :default-active="activeIndex"
      class="el-menu-demo"
      mode="horizontal"
      router
    >
      <el-menu-item  v-for="navItme in navList" :index="navItme.path" :key="navItme.index">{{navItme.name}}</el-menu-item>
    </el-menu>
  </div>
</template>
<script>
export default {
  name: "",
  components: {},
  data() {
    return {
      navList: [
        {
          idnex: 1,
          name: 'Cropper',
          path: 'home'
        },
        {
          idnex: 2,
          name: 'vue-Cropper',
          path: 'about'
        },
        {
          idnex: 3,
          name: 'UEditor',
          path: 'uedit'
        },
      ],
      activeIndex: 'uedit'
    };
  },
  computed: {},
  created() {},
  mounted() {},
  methods: {},
};
</script>

<style scoped lang="scss"></style>
