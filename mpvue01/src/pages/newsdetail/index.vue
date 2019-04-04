<template>
  <div>
    {{list.title}}
    <div v-html="list.content"></div>
  </div>
</template>

<script>
export default {
  components: {

  },

  data () {
    return {
        list:[],
    }
  },
methods:{
    requestData(aid){
      var that=this;
      var url= "http://www.phonegap100.com/appapi.php?a=getPortalArticle&aid="+aid;
      wx.request({
        url: url, //仅为示例，并非真实的接口地址
        header:{
          "Content-Type":"application/json"
        },
        success: function(res) {
          console.log(res.data.result)
          that.list=res.data.result[0];
        }
      })
    }
},
  onLoad(options){//微信小程序接收上一个页面传过来的参数
    //console.log(options)//options就是参数
    this.requestData(options.aid)
  },
  created () {
    //this.requestData();
  }
}
</script>

<style scoped>
  li{
    height:60px;
    border-bottom : solid 1px #333;
  }

</style>
