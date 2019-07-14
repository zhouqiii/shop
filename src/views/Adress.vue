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
<div :style="adressCart1" >
<div :style="adressContent">
  <span>JackBean<i class="el-icon-edit" style="margin-left:45%;"></i></span>
  <p style="font-size:14px;">地址</p>
  <p style="font-size:14px;margin-top:30px;color:Gray;">12345</p>
  <p style="color:#D2691E;font-size:14px;">默认地址</p>
</div>
</div>
<div :style="adressCart2" >
<i class="el-icon-plus"></i>
<p>添加新地址</p>
</div>
<div :style="adressCart3" >
  <span>more<i class="el-icon-arrow-down"></i></span>
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
      adressCart1: {
        border: '2px solid LightGrey',
        height: '180px',
        width: '22%',
        margin: '35px 10px 10px 0px',
        position: 'absolute'
      },
        adressCart2: {
        border: '2px solid LightGrey',
        height: '180px',
        width: '22%',
        margin: '35px 10px 10px 25%',
        position: 'absolute'
      },
      adressCart3: {
      position: 'absolute',
      marginTop: '18%',
      color: '#D2691E',
      marginLeft: '47%'
      },
      adressContent: {
       textAlign: 'left',
       paddingTop: '20px',
       paddingLeft: '18px',
       fontSize: '18px'
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
div .el-icon-edit{
  font-size: 25px;
};
div .el-icon-plus{
  font-size: 60px;
  margin-top: 13%;
}
</style>


