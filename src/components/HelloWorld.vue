<template>
  <div>
    <h3>抽奖环节</h3>
    <el-input v-model="count" placeholder="请输入要抽奖的人数" @input="init"></el-input>
    <p></p>
    <el-carousel ref="carousel" type="card" height="200px" indicator-position="none" :autoplay="autoplay" arrow="never">
      <el-carousel-item v-for="item in list" :key="item" name="item">
        <h1>{{ item + 1 }}</h1>
      </el-carousel-item>
    </el-carousel>
    <p></p>
    <el-button type="primary" round style="width: 100%;" @click="change">抽取</el-button>
    <p></p>
    <el-button type="primary" round style="width: 100%;" @click="init">重置</el-button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      list: [],
      expectList: [],
      autoplay: false,
      count: '',
      lastIndex: -1
    }
  },
  created () {
    this.init()
  },
  methods: {
    change () {
      console.log('list:' + this.list)
      console.log('expect list:' + this.expectList)
      if (this.list.length === this.expectList.length) {
        alert('当前号已被抽完')
        return
      }
      while (true) {
        let randomIndex = this.randomNum(0, this.list.length - 1)
        if (this.expectList.indexOf(randomIndex) === -1) {
          this.expectList.push(randomIndex)
          let num = this.list[randomIndex]
          this.$refs.carousel.setActiveItem(num)
          this.lastIndex = randomIndex
          return
        }
      }
    },
    randomNum (minNum, maxNum) {
      switch (arguments.length) {
        case 1:
          return parseInt(Math.random() * minNum + 1, 10)
        case 2:
          return parseInt(Math.random() * (maxNum - minNum + 1) + minNum, 10)
        default:
          return 0
      }
    },
    init () {
      this.list = []
      this.expectList = []
      for (let i = 0; i < this.count; i++) {
        this.list.push(i)
      }
    }
  }
}
</script>

<style>
  .el-carousel__item h1 {
    color: blue;
    font-size: 20px;
    opacity: 0.75;
    line-height: 200px;
    margin: 0;
  }

  .el-carousel__item:nth-child(2n) {
    background-color: #67C23A;
  }

  .el-carousel__item:nth-child(2n+1) {
    background-color: #E6A23C;
  }
</style>
