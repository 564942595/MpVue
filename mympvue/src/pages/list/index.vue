<template>
  <div>
     <ul class="mui-table-view mui-table-view-striped mui-table-view-condensed" v-for="(item,key) in list" :key="key" @click="toDetail(item.aid)">
            <li class="mui-table-view-cell">
                <div class="mui-table">
                    <div class="mui-table-cell mui-col-xs-10">
                        <h4 class="mui-ellipsis">{{key+1}}、{{item.title}}</h4>
                       <!--  <h5>申请人：李四</h5>
                        <p class="mui-h6 mui-ellipsis">Hi，李明明，申请交行信息卡，100元等你拿，李明明，申请交行信息卡，100元等你拿，</p>
                    </div>
                    <div class="mui-table-cell mui-col-xs-2 mui-text-right">
                        <span class="mui-h5">12:25</span> -->
                    </div>
                </div>
            </li>
          </ul>


   <!--  <ul>
      <li v-for="(item,key) in list" :key="key" @click="toDetail(item.aid)">
        {{item.title}}
      </li>
    </ul> -->
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
      wx.request({
        url: url, //仅为示例，并非真实的接口地址
        header:{
          "Content-Type":"application/json"
        },
        success: function(res) {
          console.log(res.data.result)
          that.list=res.data.result;
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
.mui-table-view-cell{line-height: 50px;}
</style>