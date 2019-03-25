<template>
  <div id="chuansuo">
    <div id="left">
      <el-checkbox-group v-model="LcheckList">
        <div v-for="item in left">
          <el-checkbox :label="item"></el-checkbox>
        </div>
      </el-checkbox-group>
    </div>
    <div id="center">
      <el-button type="primary" @click="leftFun">>>>>>>></el-button>
      <el-button type="primary" @click="rightFun" style="margin-left:0px;"
        ><<<<<<<</el-button
      >
    </div>
    <div id="right">
      <div>
        <el-checkbox v-model="checked" @change="quanxuan">全选</el-checkbox>
      </div>
      <el-checkbox-group v-model="RcheckList">
        <div v-for="item in right">
          <el-checkbox :label="item"></el-checkbox>
          <input type="text" :value="item" @change="asd($event)" />
        </div>
      </el-checkbox-group>
    </div>
  </div>
</template>

<script>
export default {
  name: "home",
  components: {},
  data() {
    return {
      checked: false,
      input: "",
      left: ["复选框 A", "复选框 B", "复选框 C"],
      right: ["复选框 D", "复选框 E", "复选框 F"],
      LcheckList: ["复选框 A"],
      RcheckList: ["复选框 D"]
    };
  },
  methods: {
    asd: function(e, v) {
      this.$set(
        this.right,
        this.right.indexOf(e.target._value),
        e.target.value
      );
    },
    leftFun: function() {
      for (let i = 0; i < this.LcheckList.length; i++) {
        this.left.splice(this.left.indexOf(this.LcheckList[i]), 1);
        this.right.push(this.LcheckList[i]);
      }
      this.LcheckList = [];
    },
    rightFun: function() {
      for (let i = 0; i < this.RcheckList.length; i++) {
        this.right.splice(this.right.indexOf(this.RcheckList[i]), 1);
        this.left.push(this.RcheckList[i]);
      }
      this.RcheckList = [];
    },
    quanxuan: function() {
      if (this.checked) {
        this.RcheckList = this.right;
      }else{
        this.RcheckList=[];
      }
    }
  },
  watch: {
    RcheckList: {
      handler: function() {
        if(this.RcheckList.length==this.right.length){
          this.checked=true;
        }else{
          this.checked=false;
        }
      },
      deep: true
    }
  }
};
</script>
<style>
#chuansuo {
  display: flex;
}
#left {
  width: 200px;
  height: 500px;
}
#center {
  width: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
#right {
  width: 400px;
  height: 500px;
}
</style>

