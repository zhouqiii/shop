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
     <div>
        <ul style="padding-inline-start:0px;">
            <div v-for="(item,index) in lists" :key="index" style="border:1px solid #A9A9A9;height:70px;">
                <dl>
                    <dd :style="btn" ><input type="checkbox" v-model="item.check" @click="choose(item)"/></dd>
                    <dd :style="image"><img :src="item.productImage"></dd>
                    <dd :style="proame">{{item.productName}}</dd>
                    <dd :style="give" v-for="(part,index) in item.parts" :key="index">赠送：{{part.partsName}}</dd>
                    <dd :style="price">{{item.productPrice | formatMoney}}</dd>
                    <dd :style="number">
                        <span>
                            <span @click="add(item,1)">+</span>
                            <input type="text" value="0" v-model="item.productQuantity" style="width:30px;margin:0 5px;"/>
                            <span @click="add(item,-1)">-</span>
                        </span>
                    </dd>
                    <dd :style="priceAdd">{{item.productPrice * item.productQuantity | formatMoney}}</dd>
                    <dd :style="del" ><i class="el-icon-delete" @click="show"></i></dd>
                </dl>
            </div>
        </ul>
     </div>
    </div>
     <div style="text-align:left;margin:30px 20px 0px 20px;">
         <input type="checkbox" :class="{'check':checkAllFlag}" @click="checkAll(true)"/>
         <span style="margin:20px 10px 0 10px;color:#D2691E;">全选</span>
         <span style="margin-right:66%;" @click="checkAll(false)">取消全选</span>
         总额：<span style="color:#B22222;">{{totalMoney | formatMoney}}</span>
         <div :style="money">付款</div>
     <!--<table style="width:100%;vertical-align:center;">
       <tr>
       <td><input type="checkbox"/></td>
       <td style="margin-right:10px;">全选</td>
       <td>取消全选</td>
       <td>付款：</td>
       <td style="width:17%;height:10%;background-color:red;">结账</td> 
       </tr> -->
    </div>
    <div>
        <Delete v-show="showAlert" @hidden="hiddenShow" @delete="deleteData(index)" ></Delete>
    </div>
</div>
</template>

<script>
// @ is an alias to /src
import dataJson from './cart.json'
import Delete from '../components/Delete.vue'

export default {
  name: 'cart',
  components:{
      Delete
  },
  data () {
      return{
           lists: [],
           part: [],
           list: [],
           checkAllFlag: false,
           showAlert: false,
           totalMoney: 0,
           content:{
            height: ''
           },
           project: {
               height: '50px',
               backgroundColor: 'DimGray',
               border: '1px solid  #A9A9A9',
               paddingTop: '15px'
           },
           btn:{
               margin: '0 auto',
               paddingTop: '5px',
               float: 'left',
               marginLeft: '20px',
               width: '1%'
           },
           image: {
               float: 'left',
               marginLeft: '10px',
               width: '70px'
           },
           proame:{
               float: 'left',
               textAlign: 'left',
               marginLeft: '10px',
               width: '7%'
           },
           give:{
               float: 'left',
               textAlign: 'left',
               marginLeft: '10px',
               width: '35%'
           },
           price:{
               float: 'left',
               textAlign: 'left',
               marginLeft: '10px',
               width: '11%'
           },
            number: {
                float: 'left',
                textAlign: 'left',
                marginLeft: '10px',
                width: '12%'
           },
           priceAdd: {
               float: 'left',
               textAlign: 'left',
                marginLeft: '10px',
                width: '3%',
                color: 'red'
           },
           del: {
               fontSize: '20px'
           },
           money: {
               float: 'right',
               height: '40px',
               width: '15%',
               backgroundColor: '#B22222',
               paddingTop: '10px',
               textAlign: 'center',
               color: '#fff',
               textSize: '20px'
           }
      }
  },
  created () {
      this.dataView();
      this.getBor()
  },
  filters: {
    formatMoney: function (value) {
        return "￥"+value.toFixed(2);
    } 
  },
  methods: {
      dataView: function () {
      let data = dataJson;
      this.lists = data.result.list;
      },
      getBor: function () {
        // this.project.height=window.innerHeight-700+'px';
      },
      add: function (product,way) {
          if(way>0){
              product.productQuantity++;
          }else{
              product.productQuantity--;
              if(product.productQuantity<2){
                  product.productQuantity = 1;
              }
          }
          this.calcTotalMoney();
      },
      hiddenShow: function() {
      this.showAlert = false;
      },
      choose: function(item) {
           if(typeof item.check == 'undefined'){
               this.$set(item,"check",true)
           }else{
               item.check = !item.check;
           }
           this.calcTotalMoney();
       },
       checkAll: function(flag) {
           this.checkAllFlag = flag;
           var _this = this;
           this.lists.forEach(function (item,index) {
            if(typeof item.check == 'undefined'){
               _this.$set(item,"check", _this.checkAllFlag)
           }else{
               item.check = _this.checkAllFlag;
           }
           })
           this.calcTotalMoney();
       },
       calcTotalMoney: function () {
        var _this=this;
        this.totalMoney = 0;
        this.lists.forEach(function (item,index) {
         if(item.check){
           _this.totalMoney += item.productQuantity*item.productPrice;
       }   
        });
       },
       show: function () {
           this.showAlert = true;
       },
       deleteData: function (index) {
           this.lists.splice(index,1);
           this.showAlert = false;
       }
  }
}

</script>
<style lang="sass">

</style>
