<template>
  <div class="counter-warp">
  <!--轮播图地址 和搜索-->
      <div class='top'>
        <img class='bg' src='/static/images/fenxiangbg.png'>
        <img class='ewm' src='/static/images/ewm.jpg'>
      </div>
      
      <div class='footer'>
          <img @click='onShareAppMessage' src='/static/images/fenxiangicon1.png'>
          <button type="primary" open-type="share" plain="true" data-name="shareBtn">转发</button>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      userId:'',
    }
  },
  onLoad() {
      this.userinfo()
  },
  methods: {
    // 	关于平台
      userinfo(){
        this.$wxAjax('users', {
            userToken: this.$getStorage('token')

          }).then((data) => {
            if (data.status == 0) {
                 this.userId = data.data.userInfo.id
            } else {
              this.$toast(data.message);
            }
          })
      },
    
  },
  onShareAppMessage: function (res) {
      console.log(res)
      return {
        title: '分享有礼',
        path: 'pages/denglu/main?id='+this.userId,
        imageUrl:'../../static/images/fenxiangtup.jpg',
        success: function (shareTickets) {
          console.info(shareTickets + '成功');
          // 转发成功
        },
        fail: function (res) {
          console.log(res + '失败');
        },
        complete:function(res){
          // 不管成功失败都会执行
        }
      }
    },
}
</script>

<style scoped>
  .logo{
    width:20%;
    margin:0 40%;
    height:1.5rem
  }
  .bg{width:75%;
margin:15px 13% 0;
height:800rpx;
}
.top{ position: relative;}
.ewm{
  position: absolute;
  left:0;
  top:0;
  right:0;
  bottom:30%;
  margin:auto;
  width:200px;height:200px
}

.footer{
}
.footer img{
  width:18%;
  padding:20rpx 17%;
  height:133rpx;
  margin-top:20rpx;

}
.footer button{
width:51%;
margin:0;
background:none;
border:none;
padding-top:120rpx;
margin-top:-154rpx;
font-weight:600;


}

</style>
