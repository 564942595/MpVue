<template>
  <div @click="clickHandle" class='home'>
   <div class="grid-content">
      <mp-grid :gridData="gridData"></mp-grid>
    </div>
        <!-- <view class="page__hd">
            <view class="page__title">Grid</view>
            <view class="page__desc">九宫格</view>
        </view>
        <view class="page__bd">
            <view class="weui-grids">
                <block wx:for="{{grids}}" wx:key="*this">
                    <navigator url="" class="weui-grid" hover-class="weui-grid_active">
                        <image class="weui-grid__icon" src="../images/icon_tabbar.png" />
                        <view class="weui-grid__label">Grid</view>
                    </navigator>
                </block>
            </view>
        </view> -->
   <!--  <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <img class="userinfo-avatar" src="/static/images/user.png" background-size="cover" />

      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
        <button>123</button>
      </div>
    </div>

    <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div>

    <form class="form-container">
      <input type="text" class="form-control" :value="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />
    </form>

    <a href="/pages/counter/main" class="counter">1去往Vuex示例页面</a>

    <div class="all">
        <div class="left">
        </div>
        <div class="right">
        </div>
    </div> -->
    <textarea name="" id="" class='cmt-text' placeholder="评价最多可输入120字..." maxlength='120' v-model="subMsg"></textarea>
    <div class='cmtCont'>
      <div class="cmtItem" v-for="(item,index) in cmtData">
        <div class="cmtTit">
          第{{index+1}}楼 &nbsp;&nbsp;
          用户{{item.user}}&nbsp;&nbsp;
          评论时间：{{item.time}}
        </div>
        <div class="cmtBody">{{item.msg}}</div>
      </div>
    </div>
    <mp-button type="primary" size="large" btnClass="mb15" @click='sub'>提交</mp-button>
  </div>
</template>

<script>
import { formatTime } from '@/utils/index'
import mpGrid from 'mpvue-weui/src/grid';
import card from '@/components/card'
//引入mpvue-weui   button组件
import mpButton from 'mpvue-weui/src/button';
import mpToast from 'mpvue-weui/src/toast';
export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      },
       gridData: [
       //app.json中使用的 路径这这里不生效，需要存在并且app.json中没使用的组件路径
        { src: '/static/images/user.png', name: '维修', url: '/pages/logs/main' },
        { src: '/static/images/user.png', name: '保养', url: '/pages/list/main' },
        { src: '/static/images/user.png', name: '年检', url: '/pages/logs/main' },
        { src: '/static/images/user.png', name: '故障', url: '/pages/logs/main' },
        { src: '/static/images/user.png', name: '工具', url: '/pages/logs/main' },
        { src: '/static/images/user.png', name: '打卡', url: '/pages/logs/main' },
      ],
      subMsg:"",
      cmtData:[
        {
          user:"匿名用户",
          msg:'这个产品还不错',
          time:'2012-12-12 12:12:12'
        }]
    }
  },

  components: {
    card,
    mpGrid,
    mpButton,
    mpToast
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    },
    sub(){
      if(this.subMsg.length==0){
        this.openToast()
      }else{
        this.cmtData.push({
          user:"匿名用户",
          msg:this.subMsg,
          time:formatTime(new Date())
        })
      }
    },
     openToast() {
      wx.showModal({
        content: '这个人很懒，什么也没说',
        //icon: 'err',
        duration: 3000
      });
    },
  },

  created () {
    // let app = getApp()
  }
}
</script>

<style scoped>
.weui-grid__label{
  font-size: 26px !important}
.home .grid-content{
  margin:15px 0 ;
}
.cmt-text{font-size: 18px;height:100px;}
.cmtTit{font-size: 15px;line-height:50px;background-color: #999;}
.cmtBody{line-height: 50px;font-size: 15px;text-indent: 20px;}
</style>
