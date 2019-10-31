<template>
<div>
  <el-carousel :interval="9000" type="card" :height="bannerHeight+'px'">
    <el-carousel-item v-for="item in imgUrls" :key="item.id">
      <el-row align="center">
        <img ref="bannerHeight" :src="item.idView" align="center" @load="imgLoad">
      </el-row>
    </el-carousel-item>
  </el-carousel>
<el-row>
  <el-col :span="24"><div class="grid-content bg-purple-dark"><h1 align="center">古生物谱系树构建系统</h1></div></el-col>
  <el-col :span="24"><div class="grid-content bg-purple-dark"><h3 align="center">提供关于古生物形态学数据的插补与层次推断建树方法，同时提供数据存储和相关论文检索功能</h3></div></el-col>
</el-row>
</div>
</template>

<script>
import { mapGetters } from "vuex";
// import adminDashboard from "./admin";
// import editorDashboard from "./editor";

export default {
  name: "主页",
  // components: { adminDashboard, editorDashboard },
  data() {
    return {
      currentRole: "adminDashboard",
      bannerHeight: 500,
      imgUrls: [
        { id: 1, idView: require("@/assets/main_images/进化图.png") },
        { id: 2, idView: require("@/assets/main_images/恐龙.png") },
        { id: 3, idView: require("@/assets/main_images/团队情况.png") },
        { id: 4, idView: require("@/assets/main_images/滇虫.png") },
        { id: 5, idView: require("@/assets/main_images/滇虫化石.png") }
      ]
    };
  },
  methods: {
    imgLoad() {
      this.$nextTick(() => {
        console.log(this.$refs.bannerHeight[0].height);
        this.bannerHeight = this.$refs.bannerHeight[0].height;
      });
    }
  },
  mounted() {
    this.imgLoad();
    window.addEventListener(
      "resize",
      () => {
        this.bannerHeight = this.$refs.bannerHeight[0].height;
        this.imgLoad();
      },
      false
    );
  },
  computed: {
    ...mapGetters(["roles"])
  },
  created() {
    if (!this.roles.includes("admin")) {
      this.currentRole = "editorDashboard";
    }
  }
};
</script>
<style>
img {
  object-fit: cover;
}
</style>
