<template>
    <div>
      <!-- 渲染 -->
        <!-- <select name="" id="" v-model="languageGroup">
            <option value="en">English</option>
            <option value="zh">Chinese</option>
        </select> -->
        <p class="_text">
            <span>请选择需要翻译的语言:</span> 
            <el-select v-model="languageGroup" size="small">
                <el-option value="en">English</el-option>
                <el-option value="zh">Chinese</el-option>
            </el-select>
            <el-button type="primary" @click="translatorCon" size="small">翻译</el-button>
        </p>
        <p class="icon">
            <el-input type="textarea" :autosize="{ minRows: 10, maxRows: 20}" placeholder="请输入内容" v-model="content" clearable></el-input>
            <i class="el-icon-circle-close-outline" id="_icon" @click="clearCon"></i>
        </p>
    </div>
</template>
<script>
export default {
  data() {
    return {
      content: "",
      languageGroup: "zh"
    };
  },
  methods: {
    translatorCon() {
      //获取用户输入的val
      let _val = this.content;
      let _langGroup = this.languageGroup;
      // console.log(_langGroup)
      //发送数据到父组件
      this.$emit("contentText", _val, _langGroup);
    },
    clearCon(){
        this.content = "";
        // console.log(_val)
    }
  }
};
</script>
<style scoped lang="less">
    ._text {
        span {
            color: cornflowerblue;
        }
        .el-button {
            width: 100px;
        }
    }
    .icon {
        position: relative;
        #_icon {
            font-size: 20px;
            position: absolute;
            right: 5px;
            top: 5px;
            cursor: pointer;
            // display: none;
        }
        #_icon:hover {
            color: #ccc;
        }
    }
    
</style>
