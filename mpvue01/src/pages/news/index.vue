<template>
  <div>
    <ul>
      <li v-for="(item,key) in list" :key="key" @click="toDetail(item.aid)">
        {{item.title}}
      </li>
    </ul>
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
    requestData(){
      var that=this;
      var url="http://www.phonegap100.com/appapi.php?a=getPortalList&catid=20&page=1";
      //var url="http://localhost:54922/MaintenceApi/Modify?type=GetAlarmClassType&us=E2EMIZmPqGnBm1bAX8nH/s5L8rqffrZcxFw+1J+TFDsq0pNaD4ziwB4VlgK5OMo4ihWaV3OeNY9H/AUgl5CEsA==";
      wx.request({
        url: url, //仅为示例，并非真实的接口地址
        header:{
          "Content-Type":"application/json"
        },
        success: (res)=> {
          console.log(res.data.result);
          this.list=res.data.result;
        }
      })
    },
  toDetail(aid){
    const url = '../newsdetail/main?aid='+aid
    mpvue.navigateTo({ url })
  }
},
  created () {
    this.requestData();
  }
}
</script>

<style scoped>
  li{
    height:60px;
    border-bottom : solid 1px #333;
  }
</style>
