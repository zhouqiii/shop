<template>
<div class="cart">  
    <div class="title">
    <el-divider content-position="center"><span style="font-size:22px;">购物车</span></el-divider>
    </div>
    <div class="content">
     <div class="project">

     </div>
     <div>
        <ul>
        <li></li>
        </ul>
     </div>
     
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
           lists: []
      }
  },
  created () {
      this.dataView();
  },
  methods: {
      dataView: function () {
      let data = dataJson;
      this.lists = data.result.list;
      }
  }
}
</script> 
<style lang="sass">
.cart{
    content{
        project{
            width:100px;
            height:60px;
            boder:1px black solid
        }
     
    }
}
</style>
