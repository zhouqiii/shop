<template>
  <div class="cart">
  <ul>
      <li v-for='(item,index) in lists' :key='index'>{{item.productName}}</li>
  </ul>
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
  methods:{
      dataView: function (dataJson) {
          debugger;
      this.lists = dataJson.result.list;//就这句话错
      }
  }
  
}
</script>
