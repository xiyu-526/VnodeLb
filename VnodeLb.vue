<template>
  <div ref="list" class="iztVnode-container" @scroll="scrollEvent($event)">
    <div class="iztVnode-wall" :style="{ height: listHeight + 'px' }" />
    <ul class="iztVnode" :style="{ transform: getTransform }">
      <slot :vDota="showData" :config="config" />
    </ul>
  </div>
</template>
<script>
export default {
  name: 'VnodeLb',
  props: {
    config: {
      type: Object,
      default: () => {
        return {
          itemHeight: 50, // 滚动行高度 默认50
          sCro: 1, // 0:禁止自动上下滚动，默认为1
          startsCro: 1, // 控制什么时候开始 1
          overFlow: 1 // 0不允许手指或者鼠标滑动  默认1
        }
      }
    },
    // 所有列表数据
    lukyPerson: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      // 循环滚动到底插入现有数组数据索引
      turnPage: 0,
      // 可视区域高度
      screenHeight: 0,
      // 偏移量
      y: 0,
      // 开始
      start: 0,
      // 结束
      end: null
    };
  },
  computed: {
    // 列表对应Wall的高度
    listHeight() {
      return this.lukyPerson.length * this.config.itemHeight;
    },
    // 可显示的列表项数
    visibleCount() {
      return Math.ceil(this.screenHeight / this.config.itemHeight) + 1;
    },
    // 偏移量
    getTransform() {
      return `translate3d(0,${this.y}px,0)`;
    },
    // 截取显示列表数据
    showData() {
      return this.lukyPerson.slice(this.start, Math.min(this.end, this.lukyPerson.length));
    },
    // 获取滚动条判断变化
    ovLfow() {
      return this.overFlow;
    }
  },
  mounted() {
    var _this = this;
    _this.$nextTick(function() {
      _this.screenHeight = document.querySelector('.iztVnode-container').clientHeight;
      _this.start = 0;
      _this.end = _this.start + _this.visibleCount;

      if (this.config.ovLfow === 0) {
        document.querySelector('.iztVnode-container').className += ' overflow';
      }

      if (this.config.sCro !== 0) {
        setInterval(() => {
          if (_this.config.startsCro === 1) {
            _this.autoMatic();
          }
        }, 50);
      }
    })
  },
  methods: {

    // 鼠标 或者 手指滑动
    scrollEvent() {
      if (this.config.startsCro === 1) {
        let scrollTop = this.$refs.list.scrollTop;
        this.start = ~~(scrollTop / this.config.itemHeight);
        this.end = this.start + this.visibleCount;
        this.y = scrollTop - (scrollTop % this.config.itemHeight);
      }
    },
    // 自动滚动
    autoMatic() {
      this.$refs.list.scrollTop += 1;
      let scrollTop = this.$refs.list.scrollTop;
      this.start = ~~(scrollTop / this.config.itemHeight);
      this.end = this.start + this.visibleCount;
      this.y = scrollTop - (scrollTop % this.config.itemHeight);

      // 滚到底之后 如果要循环滚 就把原数组数据 从头 到尾循环插入一遍
      if (this.end === this.lukyPerson.length) {
        this.lukyPerson.push(this.lukyPerson[this.turnPage]);
        this.turnPage += 1;
      }
    }
  }
};
</script>

<style scoped>
.iztVnode-container { height: 100%;  overflow-y: auto; position: relative; -webkit-overflow-scrolling: touch; }
.iztVnode-container.overflow{ overflow: hidden; }
.iztVnode-wall { position: absolute; left: 0; top: 0; right: 0; z-index: -1; visibility:hidden; opacity:0; }
.iztVnode { width:100%; left: 0; right: 0; top: 0; position: absolute; text-align: center; }
.iztVnode-item { display: block; height: 40px; overflow: hidden; font-size: 24px;}
.iztVnode-clomn1{ float: left;  width: 220px; text-align: left; color: #000000; }
.iztVnode-clomn2{ float: left;  width: 96px; color:#666666; }
.iztVnode-clomn3{ float: left; width: 155px; text-align: right; color: #c63622; }
.bscroll-indicator{ background: rgb(243, 175, 211) !important; }
</style>
