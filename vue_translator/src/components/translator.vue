<template>
  <div>
      <!-- 视图(html) -->
        <el-container>
            <el-header>
                <el-row>
                    <el-col :span="24">
                        <div class="grid-content bg-purple-dark">
                            <h1>实时翻译</h1>
                        </div>
                    </el-col>
                </el-row>
            </el-header>
            <el-main id="translatorMain">
                <el-row>
                    <el-col :span="12">
                        <div class="grid-content bg-purple">
                            <translatorFrom @contentText='contentText'></translatorFrom>
                        </div>
                </el-col>
                    <el-col :span="12">
                        <div class="grid-content bg-purple-light">
                            <translatorOutput :translatorCon="translatorCon"></translatorOutput>
                        </div>
                    </el-col>
                </el-row>
            </el-main>
        </el-container>
                    
  </div>
</template>
<script>
    import translatorFrom from './translatorChild/translatorFrom'
    import translatorOutput from './translatorChild/translatorOutput'
    export default {
        components:{
            translatorFrom,
            translatorOutput
        },
        data(){
            return{
                translatorCon:''
            }
        },
        methods:{
            contentText(data,lang){
                // console.log(lang);
                //https://translate.yandex.net/api/v1.5/tr.json/translate
                //key:trnsl.1.1.20180425T140723Z.0f326a82d6886cb8.b6b41955da685a148c00cdc2be6dc5f9a82f6038
                //lang:en
                //text
                this.axios.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180425T140723Z.0f326a82d6886cb8.b6b41955da685a148c00cdc2be6dc5f9a82f6038&lang='+lang+'&text='+data)
                .then((res)=>{
                    // console.log(res);
                    this.translatorCon = res.data.text[0]
                })
            },
        }
    }
</script>
<style scoped lang='less'>
/* scoped:接下来的样式只在当前组件生效(类似于避免js全局污染) */
    .el-row {
        width: 1200px;
        margin: auto;
    }
    .grid-content{
        h1{
            text-align: center;
            color: cornflowerblue;
        }
    }  
</style>

