<template>
<div class="adress" style="margin:0px 20px 0px 20px;">
    <!--el-step使用可以参考element官方-->
<div>
  <el-steps :active="1"  simple style="margin-bottom:5px;">
    <el-step title="地址确认" ></el-step>
    <el-step title="查看订单" ></el-step>
    <el-step title="支付" ></el-step>
    <el-step title="订单确认" ></el-step>
  </el-steps>
</div>
<div style="padding-top:20px;">
  <el-divider content-position="center">
  <span style="font-size:18px;font-weight:bold;color:SlateGray;">配送地址</span>
  </el-divider>
</div>
<div :style="adressCart" >

</div>
<div :style="adressCart" >

</div>
</div>
</template>
<script>
import AdressJson from './adress.json'

export default {
    name: 'Adress',
    data () {
      return {
      adressLists: [],
      adressCart: {
        border: '2px solid LightGrey',
        height: '180px',
        width: '22%',
        margin: '40px 10px 10px 0px'
      }
      }
    },
    created () {
     this.AdressView();
    },
    methods: {
     AdressView: function () {
       let date = AdressJson;
       this.adressLists =date.result;
     }
    }
}
</script>
<style lang="scss">

</style>


