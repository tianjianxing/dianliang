<template>
  <div class="index" :style="{height: indexHeight}">
    <div id="captureId" v-show="firstFlag">
      <div class="header">
        济南追溯
      </div>
      <div class="nav">
        <div class="navLeft">
          <div id="qrcode"></div>
          <p>追溯码</p>
          <span>{{stockNo}}</span>
        </div>
        <div class="navRight">
          <p>商品名称</p>
          <span>{{goodsName}}</span>
          <p>追溯日期</p>
          <span>{{stockTime}}</span>
          <p>追溯下载</p>
          <i @click="downLoad"><img src="../assets/下载.png" alt=""></i>
        </div>
      </div>
    </div>
    <div class="title" :style="{display: titleDiv}">
      <el-tabs class="el-tabs" v-model="activeName" @tab-click="handleClick">
        <el-tab-pane class="el-tab-pane" label="购买信息" name="first">
          <el-collapse v-model="activeNameOne" @change="handleChange">
            <el-collapse-item  name="1">
              <template slot="title">
                <i>
                  <img src="../assets/信息(1).png" alt="">
                </i>购买信息
              </template>
              <div class="contain">
                <div class="spanBox">
                  <span class="divLeft">卖家名称</span>
                  <span class="divRight">{{Purchase.shopname}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">购买价格</span>
                  <span class="divRight">{{Purchase.goodsprice}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">购买数量</span>
                  <span class="divRight">{{Purchase.goodscount}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeftThree divLeft">总金额</span>
                  <span class="divRight">{{Purchase.goodssum}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">购买日期</span>
                  <span class="divRight">{{Purchase.purchasedate}}</span>
                </div>
              </div>
              <template slot="title">
                <i class="arrow">
                  <img src="../assets/椭圆 1.png" alt="">
                </i>
              </template>
            </el-collapse-item>
          </el-collapse>
          <el-collapse v-model="activeNameTwo" @change="handleChange">
            <el-collapse-item name="1">
              <template slot="title">
                <i>
                  <img src="../assets/检测(4).png" alt="">
                </i>检测信息
              </template>
              <div class="contain">
                <div class="spanBox">
                  <span class="divLeft">检测结果</span>
                  <span class="divRight">{{Dete.results}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">检测时间</span>
                  <span class="divRight">{{Dete.detetime}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">检测机构</span>
                  <span class="divRight">{{Dete.detesgs}}</span>
                </div>
              </div>
              <template slot="title">
                <i class="arrow">
                  <img src="../assets/椭圆 1.png" alt="">
                </i>
              </template>
            </el-collapse-item>
          </el-collapse>
        </el-tab-pane>
        <el-tab-pane label="生产信息" name="second">
          <el-collapse v-model="activeNameThree" @change="handleChange">
            <el-collapse-item name="1">
              <template slot="title">
                <i>
                  <img src="../assets/生产.png" alt="">
                </i>生产者信息
              </template>
              <div class="contain">
                <div class="spanBox">
                  <span class="divLeft divLeftThree">生产者</span>
                  <span class="divRight">{{Producer.producer}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">联系方式</span>
                  <span class="divRight">{{Producer.phone}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft divLeftTwo">地址</span>
                  <span class="divRight">{{Producer.address}}</span>
                </div>
              </div>
              <template slot="title">
                <i class="arrow">
                  <img src="../assets/椭圆 1.png" alt="">
                </i>
              </template>
            </el-collapse-item>
          </el-collapse>
          <el-collapse v-model="activeNameFour" @change="handleChange">
            <el-collapse-item name="1">
              <template slot="title">
                <i>
                  <img src="../assets/环节.png" alt="">
                </i>生产环节
              </template>
              <div class="contain">
                <div class="spanBox">
                  <span class="divLeft">种植地址</span>
                  <span class="divRight">{{Link.planting_address}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft divLeftTwo">土壤</span>
                  <span class="divRight">{{Link.soil}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">种植时间</span>
                  <span class="divRight">{{Link.soildate}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">肥料品牌</span>
                  <span class="divRight">{{Link.fertilize}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft divLeftTwo">光照</span>
                  <span class="divRight">{{Link.beam}}</span>
                </div>
              </div>
              <template slot="title">
                <i class="arrow">
                  <img src="../assets/椭圆 1.png" alt="">
                </i>
              </template>
            </el-collapse-item>
          </el-collapse>
        </el-tab-pane>
        <el-tab-pane label="流通信息" name="third">
          <el-collapse v-model="activeNameFive" @change="handleChange">
            <el-collapse-item name="1">
              <template slot="title">
                <i>
                  <img src="../assets/销售.png" alt="">
                </i>批发
              </template>
              <div class="contain">
                <div class="spanBox">
                  <span class="divLeft divLeftBox">销售企业</span>
                  <span class="divRight divRightTwo">匡山综合交易农产品批发市场</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft divLeftTwo divLeftBox">地址</span>
                  <span class="divRight divRightTwo">济南市槐荫区济齐路与西外环</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft divLeftBox">企业法人</span>
                  <span class="divRight divRightTwo">王浩</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft divLeftBox">统一社会信用代码</span>
                  <span class="divRight divRightTwo">91370104792642457G</span>
                </div>
              </div>
              <template slot="title">
                <i class="arrow">
                  <img src="../assets/椭圆 1.png" alt="">
                </i>
              </template>
            </el-collapse-item>
          </el-collapse>
          <el-collapse v-model="activeNameSix" @change="handleChange">
            <el-collapse-item name="1">
              <template slot="title">
                <i>
                  <img src="../assets/批发商.png" alt="">
                </i>批发商户
              </template>
              <div class="contain">
                <div class="spanBox">
                  <span class="divLeft">商户名称</span>
                  <span class="divRight">{{Wholesale.shopname}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">联系方式</span>
                  <span class="divRight">{{Wholesale.phone}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">进场日期</span>
                  <span class="divRight">{{Wholesale.addtime}}</span>
                </div>
              </div>
              <template slot="title">
                <i class="arrow">
                  <img src="../assets/椭圆 1.png" alt="">
                </i>
              </template>
            </el-collapse-item>
          </el-collapse>
          <el-collapse v-model="activeNameSeven" @change="handleChange">
            <el-collapse-item name="1">
              <template slot="title">
                <i>
                  <img src="../assets/销售.png" alt="">
                </i>零售
              </template>
              <div class="contain">
                <div class="spanBox">
                  <span class="divLeft divLeftBox">销售企业</span>
                  <span class="divRight divRightTwo">匡山综合交易农产品批发市场</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft divLeftTwo divLeftBox">地址</span>
                  <span class="divRight divRightTwo">济南市槐荫区济齐路与西外环</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft divLeftBox">企业法人</span>
                  <span class="divRight divRightTwo">{{Retail.applyname}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft divLeftBox">统一社会信用代码</span>
                  <span class="divRight divRightTwo">{{Retail.industrial}}</span>
                </div>
              </div>
              <template slot="title">
                <i class="arrow">
                  <img src="../assets/椭圆 1.png" alt="">
                </i>
              </template>
            </el-collapse-item>
          </el-collapse>
          <el-collapse v-model="activeNameEight" @change="handleChange">
            <el-collapse-item name="1">
              <template slot="title">
                <i>
                  <img src="../assets/零售商户.png" alt="">
                </i>零售商户
              </template>
              <div class="contain">
                <div class="spanBox">
                  <span class="divLeft">商户名称</span>
                  <span class="divRight">{{Retailshop.shopname}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">联系方式</span>
                  <span class="divRight">{{Retailshop.phone}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">进场日期</span>
                  <span class="divRight">{{Retailshop.addtime}}</span>
                </div>
              </div>
              <template slot="title">
                <i class="arrow">
                  <img src="../assets/椭圆 1.png" alt="">
                </i>
              </template>
            </el-collapse-item>
          </el-collapse>
          <el-collapse v-model="activeNameNine" @change="handleChange">
            <el-collapse-item name="1">
              <template slot="title">
                <i>
                  <img src="../assets/运输.png" alt="">
                </i>运输
              </template>
              <div class="contain">
                <div class="spanBox">
                  <span class="divLeft">司机姓名</span>
                  <span class="divRight">{{Traffic.name}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">联系方式</span>
                  <span class="divRight">{{Traffic.phone}}</span>
                </div>
                <div class="spanBox">
                  <span class="divLeft">运输日期</span>
                  <span class="divRight">{{Traffic.time}}</span>
                </div>
              </div>
              <template slot="title">
                <i class="arrow">
                  <img src="../assets/椭圆 1.png" alt="">
                </i>
              </template>
            </el-collapse-item>
          </el-collapse>
        </el-tab-pane>
      </el-tabs>
    </div>
    <img class="show-img" :src="dataURL" alt="" v-show="!firstFlag">
    <h4 v-show="h4Css">长按图片保存到手机</h4>
    <i class="el-icon-arrow-left" v-show="buttonCss" @click="goBack"></i>
  </div>
</template>

<script>
import QRCode from 'qrcodejs2'
import html2canvas from 'html2canvas'

export default {
  component: { QRCode },
  data () {
    return {
      firstFlag: true,
      dataURL: '',
      titleDiv: '',
      indexHeight: '145vh',
      h4Css: false,
      buttonCss: false,
      ID: '168622',
      activeName: 'first',
      activeNameOne: ['1'],
      activeNameTwo: ['1'],
      activeNameThree: ['1'],
      activeNameFour: ['1'],
      activeNameFive: ['1'],
      activeNameSix: ['1'],
      activeNameSeven: ['1'],
      activeNameEight: ['1'],
      activeNameNine: ['1'],
      stock_Img: '',
      stockNo: '',
      stockTime: '',
      goodsName: '',
      // 检测信息
      Dete: {
      },
      // 生产环节
      Link: {
      },
      // 生产者信息
      Producer: {
      },
      // 购买信息
      Purchase: {
      },
      // 零售
      Retail: {
      },
      // 零售商户
      Retailshop: {
      },
      // 运输
      Traffic: {
      },
      // 批发商户
      Wholesale: {
      }
    }
  },
  created () {
    this.imgSRC = window.location.href
    this.firstFlag = true
  },
  mounted () {
    this.getQueryVariable('id')
    console.log(this.ID)
    this.axios({
      methods: 'get',
      url: 'http://10.0.0.243:8082/shop/getStockLog?id=' + this.ID,
      headers: {
        'Content-Type': 'application/json'
      },
      data: {
      }
    }).then(res => {
      console.log(res.data)
      if (res.data) {
        this.stockNo = res.data.stockno
        this.stockTime = res.data.stocktime
        this.goodsName = res.data.goodsname
        this.stock_Img = res.data.stock_img
        this.Dete = res.data.dete
        this.Purchase = res.data.purchase
        this.Producer = res.data.producer
        this.Link = res.data.link
        this.Wholesale = res.data.wholesale
        this.Retail = res.data.retail
        this.Retailshop = res.data.retailshop
        this.Traffic = res.data.traffic
      }
      if (res.data.dete.status === 0) {
        this.$set(this.activeNameTwo, 0, '2')
      }
      if (res.data.purchase.status === 0) {
        this.$set(this.activeNameOne, 0, '2')
      }
      if (res.data.producer.status === 0) {
        this.$set(this.activeNameThree, 0, '2')
      }
      if (res.data.link.status === 0) {
        this.$set(this.activeNameFour, 0, '2')
      }
      if (res.data.wholesale.status === 0) {
        this.$set(this.activeNameSix, 0, '2')
      }
      if (res.data.retail.status === 0) {
        this.$set(this.activeNameSeven, 0, '2')
      }
      if (res.data.retailshop.status === 0) {
        this.$set(this.activeNameEight, 0, '2')
      }
      if (res.data.traffic.status === 0) {
        this.$set(this.activeNameNine, 0, '2')
      }
    }).catch(err => {
      console.log(err)
    })
    // this.qrcode()
    this.$nextTick(function () {
      this.qrcode()
    })
  },
  methods: {
    handleClick (tab, event) {
    },
    handleChange (val) {
    },
    goBack () {
      this.$router.go(0)
    },
    getQueryVariable (variable) {
      var query = location.href
      var res = query.split('id')[1]
      var aaa = res.replace(/[^0-9]/ig,"")
      this.ID = aaa
    },
    downLoad () {
      this.$nextTick(function () {
        this.toImg()
      })
      this.titleDiv = 'none'
      this.indexHeight = '99vh'
      this.h4Css = true
      this.buttonCss = true
      // this.toImg()
    },
    qrcode () {
      let qrcode = new QRCode('qrcode', {
        width: 110,
        height: 110,
        text: 'http://10.0.0.171:8080/#/?id=' + this.ID,
        render: 'canvas' // 设置渲染方式（有table和canvas两种方式，默认canvas）
      })
      console.log(qrcode)
    },
    toImg () {
      html2canvas(document.querySelector('#captureId')).then(canvas => {
        let imgUrl = canvas.toDataURL('image/png')
        this.dataURL = imgUrl
        this.firstFlag = false
      }).catch(err => {
        console.log(err)
      })
    }
  }
}
</script>
<style scoped lang="less">
.index{
  margin: 0;
  padding: 0;
  background-color: #dcdbdc;
  margin-top: -60px;
  .show-img{
    width: 100%;
  }
  .header{
    height: 42px;
    width: 100%;
    background-color: #0a895c;
    color: #ffffff;
    font-size: 26px;
    line-height: 42px;
    font-weight: bolder;
    letter-spacing: 8px;
  }
  .nav{
    height: 160px;
    width: 94%;
    margin: auto;
    background-color: #fff;
    border-radius: 5px;
    display: flex;
    .navLeft{
      width: 55%;
      height: 150px;
      #qrcode{
        width: 110px;
        height: 110px;
        line-height: 110px;
        margin: auto;
        margin-top: 5px;
      }
      p{
        font-size: 14px;
        margin-top: 0px;
        margin-bottom: 0;
        font-weight: bolder;
        letter-spacing: 5px;
        text-align: center;
      }
      span{
        font-size: 15px;
        color: #0a895c;
        font-weight: bolder;
        text-align: center;
      }
    }
    .navRight{
      width: 45%;
      height: 150px;
      float: right;
      p{
        margin-top: 0;
        margin-bottom: 5px;
        padding-top: 5px;
        font-size: 13px;
        font-weight: bolder;
        text-align: left;
      }
      span{
        display: block;
        font-size: 15px;
        text-align: left;
        padding-left: 16%;
        font-weight: bolder;
        color: #0a895c;
      }
      i{
        img{
          float: left;
          height: 20px;
          width: 90px;
          margin-left: 16%;
        }
      }
    }
  }
  .title{
    width: 94%;
    margin: auto;
    margin-top: 5px;
    /deep/ .el-tabs__header{
      background-color: #fff;
      margin-bottom: 0;
      border-radius: 5px;
    }
    /deep/ .el-tabs__nav{
      display: flex;
      justify-content: space-around;
      width: 100%;
    }
    /deep/ .el-tabs__item.is-active{
      color: #0a895c;
    }
    /deep/ .el-tabs__item{
      font-weight: bolder;
      padding: 0;
      width: 33.3%;
    }
    /deep/ .el-tabs__active-bar{
      background-color: #0a895c;
      border-radius: 5px;
    }
    /deep/ .el-collapse{
      border-top: 2px solid #fff;
      border-top: none;
      border-bottom: none;
      border-bottom: 1px solid #fff;
      border-radius: 5px;
    }
    /deep/ .el-collapse-item__header{
      height: 42px;
      line-height: 42px;
      color: #0a895c;
      background-color: #dcdbdc;
      font-weight: bolder;
      position: relative;
      i{
        img{
          width: 15px;
          height: 15px;
          margin: 12px 2px 0;
        }
      }
      .arrow{
        display: inline-block;
        width: 70%;
        position: absolute;
        right: 5%;
        text-align: right;
      }
    }
    /deep/ .el-icon-arrow-right:before{
      content: "";
    }
    /deep/ .el-collapse-item__wrap{
      border-radius: 5px;
    }
    /deep/ .el-collapse-item__content{
      padding-bottom: 0;
      display: flex;
      div{
        span{
          display: block;
          text-align: left;
          padding-top: 5px;
          padding-bottom: 5px;
        }
        span:nth-last-child(1){
          border-bottom: none;
        }
      }
      .contain{
        width: 100%;
        .spanBox{
          border-bottom: 1px solid;
          border-bottom: 1px solid #edebeb;
          display: flex;
          .divLeft{
            width: 30%;
            margin-left: 5%;
            .divLeftTwo{
              letter-spacing: 25px;
            }
            .divLeftThree{
              letter-spacing: 7px;
            }
          }
          .divLeftBox{
            width: 40%;
          }
          .divRight{
            width: 70%;
            color: #0a895c;
          }
          .divRightTwo{
            text-align: right;
            margin-right: 5%;
          }
          .divLeftTwo{
            letter-spacing: 25px;
          }
          .divLeftThree{
            letter-spacing: 7px;
          }
        }
        .spanBox:nth-last-child(1){
          border-bottom: none;
        }
      }
    }
  }
  .el-icon-arrow-left{
    color: #fff;
    position: absolute;
    font-size: 24px;
    width: 20px;
    height: 20px;
    left: 2%;
    top: 1%;
  }
}
</style>
