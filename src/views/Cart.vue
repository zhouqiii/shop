<template>
<div class="cart">  
    <div id="title" style="margin-left:20px;margin-right:20px;">
    <el-divider content-position="center"><span style="font-size:18px;">购物车</span></el-divider>
    </div>
    <div :class="content" style="margin:10px 20px 0 20px;">
     <div v-bind:style="project">
     <table style="width:100%;vertical-align:center;">
         <tr style="color:#fff;font-size:17px;">
             <td style="width:50%;text-align:center;">商品信息</td>
             <td style="width:12.5%;text-align:left;">商品金额</td>
             <td style="width:12.5%;text-align:left;">商品数量</td>
             <td style="width:12.5%;text-align:left;">总金额</td>
             <td style="width:12.5%;text-align:left;">编辑</td>
         </tr>
     </table>
     </div>
     <div style="margin-left:0px;">
        <ul>
            <div style="border:1px solid #A9A9A9;height:100px;">
                <dl>
                    <dd :style="btn"><input type="checkbox"/></dd>
                    <dd :style="image"><img src="../img/goods-1.jpg" width="70px"/></dd>
                    <dd :style="proame">香烟</dd>
                    <dd :style="give">赠送：</dd>
                    <dd :style="price">￥8</dd>
                    <dd :style="number">
                        <span>
                            +<input type="text" value="1" style="width:30px;margin:0 5px;"/>-
                        </span>
                    </dd>
                    <dd :style="priceAdd">￥11</dd>
                    <dd :style="del"><i class="el-icon-delete"></i></dd>
                </dl>
            </div>
        </ul>
     </div>
    </div>
    <div style="text-align:left;margin:10px 20px 0 20px;">
     <table style="width:100%;vertical-align:center;">
       <tr>
        <td><input type="checkbox"/></td>
       <td style="margin-right:10px;">全选</td>
       <td>取消全选</td>
       <td>付款：</td>
       <td style="width:17%;height:10%;background-color:red;">结账</td> 
       </tr>
    </div>
</div>
</template>

<script>
// @ is an alias to /src
import dataJson from './cart.json'

export default {
  name: 'cart',
  data () {
      return{
           lists: [],
           content:{
            height: ''
           },
           project: {
               height: '',
               backgroundColor: 'DimGray',
               border: '1px solid  #A9A9A9',
           },
           btn:{
               margin: '0 auto',
               paddingTop: '25px',
               float: 'left',
               marginLeft: '10px'
           },
           image: {
               float: 'left',
               marginLeft: '10px',
               width: '72px'
           },
           proame:{
               float: 'left',
               textAlign: 'left',
               marginLeft: '10px',
               width: '72px'
           },
           give:{
               float: 'left',
               textAlign: 'left',
               marginLeft: '10px',
               width: '430px'
           },
           price:{
               float: 'left',
               textAlign: 'left',
               marginLeft: '10px',
               width: '130px'
           },
            number: {
                float: 'left',
                textAlign: 'left',
                marginLeft: '10px',
                width: '160px'
           },
           priceAdd: {
               float: 'left',
               textAlign: 'left',
                marginLeft: '10px',
                width: '60px',
                color: 'red'
           },
           del: {
               fontSize: '20px'
           }
      }
  },
  created () {
      this.dataView();
      this.getBor()
  },
  methods: {
      dataView: function () {
      let data = dataJson;
      this.lists = data.result.list;
      },
      getBor: function () {
        this.project.height=window.innerHeight-575+'px';
      }
  }
}
</script>
<style lang="sass">

</style>
