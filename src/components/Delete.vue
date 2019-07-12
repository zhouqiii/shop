<template>
  <div class="delete" :style="del">
    <p style="text-align:center;margin-top:35px;">确定删除吗？</p>
    <input type="button" style="background-color:#B22222;height:18%;width:20%;;color:#fff;margin-top:20px" value="Yes" @click="sure()"/>
    <input type="button" style="background-color:#B22222;height:18%;width:20%;;color:#fff;margin-left:40px;margin-top:20px" value="No" @click="cancel" />
  </div>
</template>

<script>
export default {
  name: 'Delete',
  data () {
    return {
      del:{
        height: '170px',
        width: '280px',
        border: '1px solid #A9A9A9',
        margin: '10px auto',
      }
    }
  },
  methods: {
    cancel: function () {
       this.$emit('hidden')
    },
    sure: function () {
     this.$emit('delete')
    }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
