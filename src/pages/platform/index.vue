<template>
  <div class="counter-warp">
  <!--轮播图地址 和搜索-->
      <img class='logo' :src='content.pic'>
      <div class='cont' v-html='content.content'></div>
  </div>
</template>

<script>
export default {
  data () {
    return {
     
      content: '',
    }
  },
  onLoad() {
      this.contents()
      
  },
  methods: {
    // 	关于平台
    contents(){
      this.$wxAjax('contents', {
        userToken:this.$getStorage('token'),
        column_id: 2,
        id:3
      }).then((data) => {
        if (data.status == 0) {
          this.content = data.data
          
        } else {
          this.$toast(data.message);
        }
      })
    },
  }
}
</script>

<style scoped>
  .logo{
    width:20%;
    margin:0 40%;
    height:1.5rem
  }
  .cont{width:90%;margin:0 5%;font-size:14px;line-height:25px;}
</style>
