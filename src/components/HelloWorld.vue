<template>
  <div class="home">
    <mt-button type="default" class="circle" @click.native="handleClick" >记一笔</mt-button>
    <mt-field label="收入" placeholder="请输入金额（支出为负数）" v-model="money" class="money"></mt-field>
    <mt-field label="用途" placeholder="请输入用途" v-model="way"></mt-field>
    <mt-field label="日期" placeholder="请输入日期" v-model="time" ></mt-field>
    <mt-button type="danger" class="keep" @click.native="handleClickKeep">保存</mt-button>

    <div v-for='(Information,index) in Informations' :key='index' class="contentCard">
      <div class="kindof-container">
        <div style='font-size:16px;'>#{{index+1}}·</div>

      </div>
    </div>


  </div>
</template>


<script>
import { Button, Field } from "mint-ui";

import axios from "axios";
export default {
  data() {
    return {
      money: "",
      way: "",
      time: "",
      Informations: []
    };
  },
  methods: {
    //getContent() {
      //let that = this;
      //axios.get("http://localhost:3000/getContent").then(function(res) {
        //console.log(res);
        //that.Informations = res.data.reverse();
      //});
    //},
    handleClick: function() {
      alert("记一笔账吧~");
    },
    handleClickKeep: function() {
      console.log("111");
      console.log(this.time);
      if (this.money === "") {
        console.log("请输入内容1");
        alert("请填写金额");
        return;
      }
      if (this.way === "") {
        console.log("请输入内容2");
        alert("请填写用途");
        return;
      }
      if (this.time === "") {
        console.log("请输入内容");
        alert("请填写日期");
        return;
      }
      var showContent = {
        income: this.money,
        date: this.time,
        use: this.way
      };
      axios.post("http://lrw.hhp.im/article", showContent).then(function(res) {
          console.log(res);
        });
      this.$router.push({'path':"/info"});
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.circle {
  height: 100px;
  width: 30%;
  border-radius: 150px;
  font-family: "黑体";
  font-weight: bolder;
  color: #fc6076;
  border: 1px solid #fc6076;
}
.money {
  top: 144px;
}
.keep {
  top: 88px;
  width: 100%;
}
.swipe {
  height: 200px;
  width: 100%;
  top: 132px;
}
.swipe1 {
  width: 100%;
  height: 210px;
}
.swipe2 {
  width: 100%;
  height: 210px;
}
.swipe3 {
  width: 100%;
  height: 210px;
}
.contentCard {
  width: 95%;
  box-sizing: border-box;
  padding: 30px 10px;
  background-color: #b3c7c7;
  margin-top: 10px;
  margin-left: 10px;
  margin-right: 10px;
  border-radius: 5px;
  font-size: 20px;
}
</style>
