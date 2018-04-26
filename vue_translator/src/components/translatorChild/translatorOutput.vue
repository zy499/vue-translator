<template>
  <div>
        <div class="textCon">
            <p>
                {{translatorCon}}
            </p>
        </div>
  </div>
</template>
<script>
    export default {
        data(){
            return{

            }
        },
        props:['translatorCon'],
        methods:{

        }
    }
</script>
<style scoped lang="less">
    .textCon {
        background-color: rgb(243, 237, 237);
        margin-top: 42px;
        height: 222px;
        p {
            padding: 10px;
            margin-bottom: 0;
        }
    }
</style>
