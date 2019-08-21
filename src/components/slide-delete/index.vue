<template>
  <div class="slide-delete">
    <div
      class="content"
      :style="{ transform: `translateX(${ctnTransformX}px)` }"
      @touchstart="touchStart"
      @touchmove="touchMove"
      @touchend="touchEnd"
    >
      <slot></slot>
    </div>
    <div
      class="delete"
      ref="delBtn"
      :style="{ transform: `translateX(${delBtnTransformX}px)` }"
    >
      <div>删除</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "slide-left-delete",
  props: [],
  data() {
    return {
      startX: null,
      delBtnWidth: null,
      slideDistance: null,
      ctnTransformX: null,
      delBtnTransformX: null
    };
  },
  mounted() {
    // 获取删除按钮的宽度
    this.delBtnWidth = this.$refs.delBtn.offsetWidth;
    // 设置初始化的按钮位置
    this.delBtnTransformX = this.delBtnWidth;
  },
  methods: {
    touchStart(evt) {
      // 触屏的初始位置
      this.startX = evt.changedTouches[0].pageX;
    },
    touchMove(evt) {
      // 触屏滑动的距离(左滑，暂时取正值)
      this.slideDistance = this.startX - evt.changedTouches[0].pageX;
      // content移动的距离
      this.ctnTransformX = `-${this.slideDistance}`;
      // delBtn移动的距离
      this.delBtnTransformX = this.delBtnWidth - this.slideDistance;
      if (this.ctnTransformX < 0) {
        /*如果是左滑动*/
        if (this.slideDistance > this.delBtnWidth) {
          this.ctnTransformX = `-${this.delBtnWidth}`;
          this.delBtnTransformX = 0;
        }
      } else {
        /*如果是右滑或者不滑动，保持目前现状*/
        this.ctnTransformX = 0;
        this.delBtnTransformX = this.delBtnWidth;
      }
    },
    touchEnd() {
      if (this.slideDistance > this.delBtnWidth * 0.6) {
        this.ctnTransformX = `-${this.delBtnWidth}`;
        this.delBtnTransformX = 0;
      } else {
        this.ctnTransformX = 0;
        this.delBtnTransformX = this.delBtnWidth;
      }
    }
  }
};
</script>
<style scoped lang="scss">
.slide-delete {
  position: relative;
  overflow: hidden;
  .content {
    width: 100%;
    height: 30px;
    background-color: yellowgreen;
    transition: transform 260ms ease;
  }
  .delete {
    width: 60px;
    height: 30px;
    position: absolute;
    right: 0;
    top: 0;
    background-color: red;
    transform: translateX(100%);
    transition: transform 260ms ease;
  }
}
</style>
