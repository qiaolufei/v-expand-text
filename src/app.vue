<template>
  <div class="expand-text" ref="expandText">
    <div v-if="!(popover && showPopoverJudge)">
      <span class="expand-text-content" :style="expandStyle">{{ text }}</span>
      <div class="expander">
        <span
          v-if="btn && showBtnJudge"
        >
          <span
            v-if="!showFull"
            class="action action-expand f-csp"
            @click.stop="showFullFn(true)"
          >
            展开
            <i v-if="btnIcon" class="el-icon-arrow-down" />
          </span>
          <span
            v-else
            class="action action-pack f-csp"
            @click.stop="showFullFn(false)"
          >
            收起
            <i v-if="btnIcon" class="el-icon-arrow-up" />
          </span>
        </span>
      </div>
    </div>
    <el-popover
      v-else
      :placement="placementC"
      trigger="hover">
      <div class="popover-content">{{ text }}</div>
      <span class="expand-text-content f-csp" :style="expandStyle" slot="reference">{{ text }}</span>
    </el-popover>
  </div>
</template>
<script>
const placements = ['top', 'top-start', 'top-end', 'bottom', 'bottom-start', 'bottom-end', 'left', 'left-start', 'left-end', 'right', 'right-start', 'right-end']
export default {
  name: 'VExpandText',
  props: {
    text: { // 文本内容
      type: String,
      default: () => ''
    },
    rows: { // 折叠显示行数
      type: Number,
      default: 3
    },
    btn: { // 展开、折叠按钮显示全文本
      type: Boolean,
      default: false
    },
    btnIcon: { // 展开、折叠icon
      type: Boolean,
      default: true
    },
    popover: { // popover显示全文本
      type: Boolean,
      default: false
    },
    placement: { // popover位置
      type: String,
      default: 'bottom'
    }
  },
  data () {
    return {
      showFull: false, // 是否展示全文本
      expandStyle: '',
      showBtnJudge: false, // 判断是否需要折叠展示按钮
      showPopoverJudge: false // 判断是否需要折叠展示popover
    }
  },
  computed: {
    row () {
      return this.rows > 0 ? this.rows : 3
    },
    placementC () {
      return placements.indexOf(this.placement) !== -1 ? this.placement : 'bottom'
    }
  },
  watch: {
    text: function () {
      this.judgeExpand()
    }
  },
  mounted () { // 判断是否需要折叠
    this.judgeExpand()
  },
  methods: {
    showFullFn (value) {
      this.expandStyle = value ? '' : `display: -webkit-box;word-break: break-all;-webkit-line-clamp: ${this.row};-webkit-box-orient: vertical;text-overflow: ellipsis;overflow: hidden;`
      this.showFull = value
    },
    judgeExpand () {
      this.showBtnJudge = false
      this.showPopoverJudge = false
      this.$nextTick(() => {
        const { row } = this
        const expandTextStyle = window.getComputedStyle(this.$refs.expandText)
        const expandTextHeight = parseFloat(expandTextStyle.height) // 获取总高度
        const expandTextLineHeight = parseFloat(expandTextStyle.lineHeight === 'normal' ? parseFloat(expandTextStyle.fontSize) * 1.2 : expandTextStyle.lineHeight) // 获取行高
        // 计算行高
        const rects = Math.ceil(expandTextHeight / expandTextLineHeight)
        if (rects <= row) { // 不需要折叠展示
          this.showBtnJudge = false
          this.showPopoverJudge = false
        } else {
          this.showBtnJudge = true
          this.showPopoverJudge = true
          this.expandStyle = `display: -webkit-box;word-break: break-all;-webkit-line-clamp: ${this.row};-webkit-box-orient: vertical;text-overflow: ellipsis;overflow: hidden;`
        }
      })
    }

  }
}
</script>

<style lang="less" scoped>
@import './index.less';
</style>
