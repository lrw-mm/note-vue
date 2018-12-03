<template>
    <div>
    <mt-header fixed title="记录" class="head">
        <router-link to="/" slot="left">
            <mt-button icon="back" >返回</mt-button>
        </router-link>
        
    </mt-header>
    

    <div v-for='(content,index) in contents' :key='index'  class="contentCard">
        <div class="content-container">
            <div style='font-size:20px;text-align:center'>----NO.{{index+1}}----</div>
            <div style='font-size:22px;margin-left:105px;margin-top:10px'>日期：{{content.date}}</div>
            <div style='font-size:22px;margin-left:105px'>收入：{{content.income}}</div>
            <div style='font-size:22px;margin-left:105px'>用途：{{content.use}}</div>
        </div>
    </div>
    
</div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      contents: []
    };
  },
  created() {},
  mounted() {
    this.get();
  },
  methods: {
    get() {
      let that = this;
      axios.get("http://lrw.hhp.im/getArticle").then(function(res) {
        console.log(res.data);
        that.contents = res.data;
        that.Informations = res.data.reverse();
      });
    },
    handleClickReturn() {
      console.log("返回成功");
      this.$router.push({ path: "/info" });
    }
  }
};
</script>

<style scoped>
.head{
    background-color:#faf7ed;
    color:#191654;
    font-size:20px;
    font-weight:bold;
    
}
.contentCard{
    width: 90%;
    box-sizing: border-box;
    padding: 30px 10px;
    background-color: #e4e5e6;
    margin-top: 30px;
    margin-bottom:-10px;
    margin-left:10px;
    margin-right:10px;
    border-radius:5px;
    font-size:10px;
    font-family:"黑体";
    color:#191654;
    border:2px solid #191654
}
.content-container{
  text-align:start;
}
</style>
