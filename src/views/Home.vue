<template>
  <div class="hello">
    <p>预览</p>

    <div class="container">
      <div class="img-container">
        <img ref="image" src="../assets/logo.png" alt="">
      </div>
      <div class="before" />
      <div class="afterCropper">
        <img :src="afterImg" alt="">
      </div>
    </div>
    <el-button
      style="margin: 30px auto;"
      type="error"
      @click="sureSava"
    >裁剪</el-button>
    <el-button
      type="primary"
      @click="cropperzoom(0.1)"
    ><i
      class="el-icon-plus"
    /></el-button>
    <el-button
      type="primary"
      @click="cropperzoom(-0.1)"
    ><i
      class="el-icon-minus"
    /></el-button>
    <el-button
      type="primary"
      @click="cropperRotate(-90)"
    ><i
      class="el-icon-refresh-left"
    /></el-button>
    <el-button
      type="primary"
      @click="cropperRotate(90)"
    ><i
      class="el-icon-refresh-right"
    /></el-button>
    <el-button type="primary" @click="cropperScaleX()">Y翻转</el-button>
    <el-button type="primary" @click="cropperScaleY()">X翻转</el-button>
    旋转度数：
    <el-input-number
      v-model="inputRotate"
      controls-position="right"
      :min="0"
      :max="360"
      @change="handleChangeRotate"
    />
  </div>
</template>

<script>
import Cropper from 'cropperjs'
import 'cropperjs/dist/cropper.css'
export default {
  name: 'HelloWorld',
  props: {
    imgFile: {
      type: String,
      default: ''
    },
    skuname: {
      type: String,
      default: ''
    },
    showScaleItem: {
      type: Object,
      default: _ => ({})
    }
  },
  data() {
    return {
      myCropper: null,
      afterImg: '',
      ScaleX: 1,
      ScaleY: 1,
      fixed: false,
      fixedBox: false,
      fixedNumber: [0, 0],
      inputRotate: 0
    }
  },
  watch: {
    showScaleItem(val, oldval) {
      if (val.x == 101) {
       this.myCropper.setAspectRatio(null)
      } else {
        if (val.x) {
          this.fixed = true
          this.fixedBox = true
          this.fixedNumber = [val.x, val.y]
        } else {
          this.fixed = false
          this.fixedBox = false
        }
        this.myCropper.setAspectRatio(val.x / val.y)
      }
    }
  },
  mounted() {
    this.init()
  },
  methods: {
    handleChangeRotate(value) {
      this.cropperrotateTo(value)
    },
    init() {
      this.myCropper = new Cropper(this.$refs.image, {
        viewMode: 1,
        dragMode: 'move',
        // initialAspectRatio: 1,
        preview: '.before',
        background: false,
        autoCropArea: 0.6,
        zoomOnWheel: true,
        aspectRatio: false
        // movable :true,
        // rotatable :true
      })
    },
    // 裁剪
    uploadImgs() {
      this.afterImg = this.myCropper
        .getCroppedCanvas({
          imageSmoothingQuality: 'high'
        })
        .toDataURL('image/jpeg')
      this.$emit('getCrop', this.afterImg)
    },
    sureSava() {
      this.afterImg = this.myCropper
        .getCroppedCanvas({
          imageSmoothingQuality: 'high'
        })
        .toDataURL('image/jpeg')
      this.$emit('upload', this.afterImg)
    },
    // 缩放
    cropperzoom(val) {
      this.myCropper.zoom(val)
    },
    // 充值
    cropperReset() {
      this.myCropper.reset()
    },
    // 移动
    croppermove(val1, val2) {
      this.myCropper.move(val1, val2)
    },
    // 旋转
    cropperRotate(val) {
      this.myCropper.rotate(val)
    },
    //绝对角度旋转
    cropperrotateTo(val) {
      this.myCropper.rotateTo(val)
    },
    // X轴翻转
    cropperScaleX() {
      this.ScaleX = -this.ScaleX
      this.myCropper.scale(this.ScaleX, 1)
    },
    // y轴翻转
    cropperScaleY() {
      this.ScaleY = -this.ScaleY
      this.myCropper.scale(1, this.ScaleY)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin-bottom: 20px;
  display: flex;

}
.before {
  width: 100px;
  height: 100px;
  overflow: hidden;
  /* 这个属性可以得到想要的效果 */
}
.img-container {
  width: 600px;
  height: 400px;
  overflow: hidden;
}
.afterCropper {
  flex: 1;
  margin-left: 20px;
  border: 1px solid salmon;
  text-align: center;
}
.afterCropper img {
  width: 150px;
  margin-top: 30px;
}
::v-deep.el-input-number {
  position: relative;
  display: inline-block;
  width: 92px;
  line-height: 38px;
}
</style>
