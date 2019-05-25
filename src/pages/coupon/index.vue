<template>
  <div class="counter-warp">
    <van-tabs :active="active">
      <van-tab title="获得优惠券">
          <div class='list' v-for='(list,key) in 5' :key='key'>
              <img class='bg' src='/static/images/yh1.jpg'>
              <div class='yhqnr'>
                <div>
                  <p class='title'>58元通用优惠券</p>
                  <p  class='cont'>描述内容 优惠券描述内容</p>
                </div>
                <p class='price'>58<span style='font-size:16px'>元</span></p>
              </div>
              <p>
                <img class='tib' src='/static/images/yh3.png'>
                <span class='tibtext'>至2019.10.11</span>
                <span class='ljlq'>立即领取<img style='width:0.4rem;height:0.5rem' src='/static/images/yh4.png'></span>
                
              </p>
          </div>
      </van-tab>
      <van-tab title="已使用优惠券">
        <div class='list' v-for='(list,key) in 5' :key='key'>
             <img class='bg' src='/static/images/yh1.jpg'>
              <div class='yhqnr'>
                <div>
                  <p class='title'>58元通用优惠券</p>
                  <p  class='cont'>描述内容 优惠券描述内容</p>
                </div>
                <p class='price' style='color:#999999'>58<span style='font-size:16px'>元</span></p>
              </div>
              <p>
                <img class='tib' src='/static/images/yh3end.jpg'>
                <span class='tibtext'>至2019.10.11</span>
                <span class='ljlq'>立即领取<img style='width:0.4rem;height:0.5rem' src='/static/images/yh4.png'></span>
                
              </p>
        </div>

      </van-tab>
      
    </van-tabs>
  </div>
</template>

<script>
export default {
  data () {
    return {
      active:0,
      shoplist:[
        {'title':'秋冬款韩版低圆领中长套头打底','shopinfo':'颜色：白色；尺码：均码；','num':'1','price':'69.00','img':'/static/images/shop/shopp8.jpg'},
        {'title':'秋冬款韩版低圆领中长款宽松套头打底秋冬款韩版低圆领中长款宽松套头打底','shopinfo':'颜色：白色；尺码：均码；','num':'1','price':'69.00','img':'/static/images/shop/shopp2.png'}
      ],
    }
  },
  methods: {
  },

}
</script>

<style scoped>
.counter-warp{
  min-height:100vh;
  background:#f7f8fa
}
.list{margin-top:10px;position: relative;}
.bg{
      
      margin:0 5%;
      width:90%;
      height:2.4rem

}
.yhqnr{
  position: absolute;
  display:flex;
  top:0.2rem;
  left:8%
}
.yhqnr .title{
  font-size:22px;
  font-weight:600;
  width: 5rem;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;
}
.yhqnr .cont{
  color:#999999;
  font-size:14px;
  width: 5rem;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;
}
.yhqnr .price{
  color:#fb2651;
  font-size:26px;
  font-weight:600;
}
.tib{width:2.2rem;height:0.4rem;position: absolute;bottom:15px;
left:40px;
}
.tibtext{color:#fff;position: absolute;bottom:18px;
left:110rpx;font-size:12px}
.ljlq{
  font-size:12px;
  color:#748ac2;
  position: absolute;bottom:18px;
  right:110rpx;
}
</style>
