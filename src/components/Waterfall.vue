<template>
  <div :class="{'waterfall-wrap': true, row: row}" ref="container">
    <template v-if="row">
        <div v-for="(item, index) of list"
          :key="index"
          class="row-item">
          <img :src="item.url" :style="{height: `${height}px`}">
        </div>
        <div :style="{height: `${height}px`}" class="last-box">
        </div>
    </template>
    <template v-else>
      <div v-for="(item, index) of list"
        :key="index"
        class="column-item">
        <img :src="item.url" alt="">
      </div>
    </template>
  </div>  
</template>
<script>
  export default {
    props: {
      list: {
        type: Array,
        required: true
      },
      row: {
        type: Boolean,
        default: false
      },
      column: {
        type: Number,
        default: 4
      },
      height: {
        type: Number,
        default: 225
      }
    },
    data () {
      return {
        itemWidth: 0,
        columnData: []
      }
    },
    mounted () {
      if (!this.row) {
        this.itemWidth = `${100 / this.column}%`
        this.$nextTick(() => {
          const boxes = this.$refs.container.getElementsByClassName('column-item')
          for (let i = 0; i < boxes.length; i++) {
            this.setElementStyle(boxes[i], this.list[i], i)
          }
        })
      }
    },
    methods: {
      setElementStyle (element, img, index) {
        const w = this.$refs.container.offsetWidth / 4
        const h = ((w - 6) / img.width) * img.height + 6
        if (index < this.column) {
          element.style.left = `${index * (100 / this.column)}%`
          this.columnData[index] = this.columnData[index] ? this.columnData[index] + h : h
        } else {
          // 找出最小高度的列
          let min = {}
          for (let i = 0; i < this.columnData.length; i++) {
            if (!min.hasOwnProperty('index')) {
              min = {index: i, value: this.columnData[i]}
            } else {
              if (this.columnData[i] < min.value) {
                min = {index: i, value: this.columnData[i]}
              }
            }
          }
          element.style.left = `${min.index * (100 / this.column)}%`
          element.style.top = `${min.value}px`
          this.columnData[min.index] += h
        }
        element.style.width = this.itemWidth
      }
    }
  }
</script>
<style lang="scss" scoped>
  .waterfall-wrap {
    position: relative;
    .column-item {
      position: absolute;
      padding: 3px;
      font-size: 0;
      box-sizing: border-box;
      img {
        max-width: 100%;
      }
    }
    &.row {
      display: flex;
      flex-wrap: wrap;
      .row-item {
        margin: 5px;
        flex-grow: 1;
        font-size: 0;
        box-sizing: border-box;
        img {
          min-height: 100%;
          min-width: 100%;
          object-fit: cover;
        }
      }
      .last-box {
        margin: 5px;
        flex-grow: 999;
      }
    }
  }
</style>
