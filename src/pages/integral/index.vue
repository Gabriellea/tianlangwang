<template>
  <div class="counter-warp">
    <div class='header'>
      <img class='bg' src='/static/images/wd_00.png'>
      <div class='header_left'>
        <img :src='userinfo.headimgurl'>
        <div class='username'>
          <p>{{userinfo.nickname}}</p>
        </div>        
      </div>
      <div class='header_right'>
        <p >当前积分</p>
        <p style='font-size:24px'>{{userinfo.points}}</p>
      </div>
    </div>
    <div class='jifenfenlei'>
      <div class='jifenitem' @click='jifenxuanze(1)'>
        <img src='/static/images/jifen1.jpg'>
        <p>使用积分</p>
      </div>
      <div class='jifenitem' @click='jifenxuanze(2)'>
        <img src='/static/images/jifen2.jpg'>
        <p>获取积分</p>
      </div>
      <div class='jifenitem' @click='jifenxuanze(3)'>
        <img src='/static/images/jifen3.jpg'>
        <p>积分规则</p>
      </div>
    </div>
    <p class='jifentitle'>{{jifentitle}}</p>
    <div class='xiangqing' v-if='type==1||type==3'>
      1、帮助中心新手入门 百科理念 编辑宝典 常见问题 百科术语 编辑规则辑词条 新手入门编辑词条 只需四步 1发现问题,编辑词条
      2、帮助中心新手入门 百科理念 编辑宝典 常见问题 百科术语 编辑规则1 新手入门编辑词条 只需四步 1发现问题,编辑词条 如
      3、帮助中心新手入门 百科理念 编辑宝典 常见问题 百科术语 编辑规则1 新手入门编辑词条 只需四步 
    </div>
    <div v-else>
      <van-cell v-for='(item,index) in explainList' :key='index' :title="item.remark" :value="item.points" :label="item.change_time" border="false" />
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      userinfo:[],
      jifentitle:'使用积分',
      explain:[],
      type:1,
      explainList:[]
    }
  }, 
  onLoad() {
      this.getUserInfo();
      this.useExplain()
      this.ExplainList()
  },
  methods: {
     getUserInfo() {
      this.$wxAjax('users', {
        userToken: this.$getStorage('token')
      }).then((data) => {
        if (data.status == 0) {
          this.userinfo = data.data.userInfo;
        } else {
          this.$toast(data.message);
        }
      })
    },
    jifenxuanze(index){
      this.type = index
      if(index==1){
        this.jifentitle = '使用积分'
      }else if(index==2){
        this.jifentitle = '获取积分'
      }else{
        this.jifentitle = '积分规则'
      }
    },
    //	使用说明
    useExplain() {
      this.$wxAjax('contents', {
        userToken: this.$getStorage('token'),
        column_id: 2,
        id:4	
      }).then((data) => {
        if (data.status == 0) {
          this.explain = data.data
        } else {
          this.$toast(data.message);
        }
      })
    },
    //	使用说明
    ExplainList(){
      this.$wxAjax('pointsRecord', {
        userToken:this.$getStorage('token')
      }).then((data) => {
        if (data.status == 0) {
          this.explainList = data.data.list
        } else {
          this.$toast(data.message);
        }
      })
    },
  },
  created () {

  }
}
</script>
<style scoped>
.counter-warp{background:#f5f5f5;min-height:100vh;}
.header{height:100px;position:relative;width:100%;padding-top:10px;background:#fff}
.bg{width:90%;height:100%;position:absolute;left:0;right:0;margin:0 5%;border-radius:10px;}
.header_left{position:absolute;left:30px;top:40px;font-size:16px;color:#fff;display:flex}
.header_left img{width:1rem;height:1rem;border-radius:50%;border:2px solid #fff} 
.username{
  margin:12px 10px
}
.header_right{position:absolute;right:20px;top:35px;font-size:14px;padding:5px 10px;color:#fff;}
.jifenfenlei{display:flex;justify-content:space-between;width:96%;padding:0 2% 10px;background:#fff}
.jifenitem{width:33.33%}
.jifenitem img{width:40%;margin:0.6rem 30% 0;height:0.8rem}
.jifenitem p{text-align:center;font-size:14px}
.jifentitle{padding:10px 20px;font-size:14px;color:#e31100;font-weight:600}
.xiangqing{background:#fff;padding:15px;font-size:14px }
</style>
