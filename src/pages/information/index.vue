<template>
  <div class="counter-warp">
    <div class='header'>
      <div class='header_left'>
        <img :src='getUserInfos.headimgurl'>
        <div class='username'>
          <p>用户名内容</p>
          <p class='dengji'>普通会员</p>
        </div>
        
      </div>
    </div>
    <div style='margin:10px 0'>
      <div class='list'>
        <img src='/static/images/infomition1.png'>
        <span class='bianji'>用户名</span>
        <span class='bianjiinput'>13161663575</span>
      </div>
      <div class='list' @click="$go('phone')">
        <img style='padding:0 3px 0 1px;width:16px' src='/static/images/infomition2.png'>
        <span class='bianji'>联系方式</span>
        <span class='bianjiinput'>13161663575<van-icon style='float:right;margin-top:2px' name="arrow" /></span>
      </div>
      
    </div>
    <div class='list'  @click="$go('address')" >
      <img style='padding:0 3px 0 1px;width:16px' src='/static/images/infomition3.png'>
      <span class='bianji'>地址</span>
      <span class='bianjiinput'>{{address}}<van-icon style='float:right;margin-top:2px;' name="arrow" /></span>
    </div>
  </div>
  
</template>

<script>

export default {
  data () {
    return {
      message:'',
      phone:'',
      username:'',
      address:'点击选择地址',
      getUserInfos:[]
    }
  },
  onShow: function () {   
    this.address = '点击选择地址'
    this.seleaddress();  
    this.getUserInfo();   
  },
  methods: {
    getUserInfo() {
      this.$wxAjax('users', {
        userToken: this.$getStorage('token')
      }).then((data) => {
        if (data.status == 0) {
          console.log(data)
          this.getUserInfos = data.data.userInfo;
          
        } else {
          this.$toast(data.message);
        }
      })
    },
      //查询地址；
    seleaddress(){
      this.$wxAjax('userDefAddr', {
        userToken: this.$getStorage('token')
      }).then((data) => {
        console.log(data.data)
        if(data.data){
          this.address = data.data.province_h +'-'+ data.data.district_h +'-'+ data.data.city_h
        }
      })
    },
  },

  created () {
  }
}
</script>

<style scoped>

.counter-warp{background:#f8f8f8;height:100vh}
.header{height:1.8rem;position:relative;background:#fff}
.bg{width:100%;height:100%;position:absolute;left:0;right:0}
.header_left{position:absolute;left:20px;top:10px;font-size:16px;color:#333;display:flex}
.header_left img{width:1.2rem;height:1.2rem;border-radius:50%} 
.username{
  margin:5px 10px 10px
}
.header_right{position:absolute;right:10px;top:35px;font-size:14px;padding:5px 10px;background:rgba(0,0,0,0.5);color:#fff;border-radius:12px}
.dengji{
  font-size:12px;
  border:1px solid #fd8800;
  padding:4px 10px;
  border-radius:10px;
  text-align:center;
  color:#fd8800;
  margin:8px 0 0 0;
}
.list{background:#fff;font-size:14px;padding:15px 0 15px 15px;height:20px;border-bottom:#e6e6e6}
.bianji{width:60px;float:left;height:20px;line-height:20px}
.list img{width:20px;height:20px;margin:0 10px 0 10px;float:left}
.bianjiinput{height:20px;line-height:20px;float:left;display:block;min-height:20px;width:calc(100% - 115px);
text-align:right;overflow:hidden;
}
</style>
