<template>
  <div>
      <div class="banner-text">
        <span>
          <img src="https://img.shields.io/badge/Spring%20Boot-2.1.3.RELEASE-yellowgreen.svg" alt="Downloads">
          <img src="https://img.shields.io/badge/Spring%20Cloud-Greenwich.RELEASE-blue.svg" alt="Coverage Status">
        </span>
        <br/>
        <span>
          <el-collapse v-model="activeNames">
            <el-collapse-item title="微服务架构" name="1">
              <div>基于Spring Cloud Greenwich.RELEASE</div>
              <div>基于Spring Boot 2.1.3.RELEASE</div>
            </el-collapse-item>
            <el-collapse-item title="微服务调用" name="2">
              <div>RPC协议</div>
              <div>GRPC框架</div>
            </el-collapse-item>
            <el-collapse-item title="亮点功能" name="3">
              <div>代码生成器</div>
              <div>乐观锁</div>
              <div>逻辑删除</div>
              <div>Docker部署</div>
            </el-collapse-item>
          </el-collapse>
        </span>
      </div>
  </div>
</template>

<script>
  import {mapGetters} from 'vuex';

  export default {
    name: 'wel',
    data() {
      return {
        activeNames: ['1', '2', '3', '4'],
        DATA: [],
        text: '',
        actor: '',
        count: 0,
        isText: false
      }
    },
    computed: {
      ...mapGetters(['website'])
    },
    methods: {
      getData() {
        if (this.count < this.DATA.length - 1) {
          this.count++
        } else {
          this.count = 0
        }
        this.isText = true
        this.actor = this.DATA[this.count]
      },
      setData() {
        let num = 0
        let count = 0
        let active = false
        let timeoutstart = 5000
        let timeoutend = 1000
        let timespeed = 10
        setInterval(() => {
          if (this.isText) {
            if (count === this.actor.length) {
              active = true
            } else {
              active = false
            }
            if (active) {
              num--
              this.text = this.actor.substr(0, num)
              if (num === 0) {
                this.isText = false
                setTimeout(() => {
                  count = 0
                  this.getData()
                }, timeoutend)
              }
            } else {
              num++
              this.text = this.actor.substr(0, num)
              if (num === this.actor.length) {
                this.isText = false
                setTimeout(() => {
                  this.isText = true
                  count = this.actor.length
                }, timeoutstart)
              }
            }
          }
        }, timespeed)
      }
    }
  }
</script>

<style scoped="scoped" lang="scss">
  .wel-contailer {
    position: relative;
  }

  .banner-text {
    position: relative;
    padding: 0 20px;
    font-size: 20px;
    text-align: center;
    color: #333;
  }

  .banner-img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0.8;
    display: none;
  }

  .actor {
    height: 250px;
    overflow: hidden;
    font-size: 18px;
    color: #333;
  }

  .actor:after {
    content: '';
    width: 3px;
    height: 25px;
    vertical-align: -5px;
    margin-left: 5px;
    background-color: #333;
    display: inline-block;
    animation: blink 0.4s infinite alternate;
  }

  .typeing:after {
    animation: none;
  }

  @keyframes blink {
    to {
      opacity: 0;
    }
  }
</style>
