<template>
  <div class="counter-warp">
    <van-tabs :active="active"  @change="onChange">
      <van-tab title="我的分销">
        <scroll-view
          scroll-y
          style="height:100vh"
          bindscrolltoupper="upper"
          bindscrolltolower="lower"
          bindscroll="scroll"
          scroll-top="100"
          @scrolltolower='scrollfun'
        >
          <div class='list' @click="$go('personnellist',{id:1})">
            <div class='item'>
              <van-icon style='color:#cbcbcb;float:left;margin-top:3px;margin-right:4px;' name="arrow" />
              <span>成功分销</span>
            </div>
            <span class='remshu'>0人</span>
          </div>
        </scroll-view>
      </van-tab>
      
      <van-tab title="我的佣金">
        <scroll-view
          scroll-y
          style="height:100vh"
          bindscrolltoupper="upper"
          bindscrolltolower="lower"
          bindscroll="scroll"
          scroll-top="100"
          @scrolltolower='scrollfun'
        >
          <div class='header'>
            <img class='bg' src='/static/images/wd_00.png'>
            <div class='header_right'>
              <p >当前积分</p>
              <p style='font-size:24px'>88822228.99</p>
            </div>
            <span class='header_left' @click="$go('wallet',{id:1})">申请提现</span>
            <div style='height:20px'></div>
          </div>
          <p class='yjtitle'>佣金明细</p>
          <div>
             <van-cell title="单元格" value="内容" label="描述信息" />
             <van-cell title="单元格" value="内容" label="描述信息" />
             <van-cell title="单元格" value="内容" label="描述信息" />
             <van-cell title="单元格" value="内容" label="描述信息" />
             <van-cell title="单元格" value="内容" label="描述信息" />
             <van-cell title="单元格" value="内容" label="描述信息" />
          </div>
      </scroll-view>
      </van-tab>
    </van-tabs>
  </div>
</template>

<script>
export default {
  data () {
    return {
      userinfo:[]
    }
  },
  onShow: function () {   
     this.getUserInfo()
  },
  methods: {   
    getUserInfo() {
      this.$wxAjax('fenxiaos', {
        userToken: this.$getStorage('token')
      }).then((data) => {
        if (data.status == 0) {          
          this.userinfo = data.data.userInfo;          
        } else {
          this.$toast(data.message);
        }
      })
    },
  },

}
</script>

<style scoped>
.header{height:140px;position:relative;width:100%;padding-top:10px;background:#fff}
.bg{width:90%;height:80%;position:absolute;left:0;right:0;margin:0 5%;border-radius:10px;}
.header_left{position:absolute;right:30px;top:55px;font-size:14px;color:#ff4842;padding:4px 10px;background:#fff;border-radius:8px}
.header_left img{width:1rem;height:1rem;} 
.yjtitle{color:#e31100;font-size:14px;font-weight:600;padding-left:15px;line-height:40px}
.header_right{position:absolute;left:30px;top:35px;font-size:14px;padding:5px 10px;color:#fff;}
.counter-warp{
  min-height:100vh;
  background:#f8f8f8
}
.remshu{
  padding:3px 15px;background:#fa4319;color:#fff;border-radius:15px;font-size:14px;
}
.list{
  display:flex;
  justify-content:space-between;
  padding:10px 15px;
  font-size:14px;
  background:#fff
}
</style>
