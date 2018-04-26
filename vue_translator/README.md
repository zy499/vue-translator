MVVM:数据变化引起试图变化

vue指令：
v-text：只以文本方式渲染数据
v-html：可渲染数据中的html标签
v-once：只渲染一次，直接加在元素上，无表达式
v-show：赋值true/false，控制dom的隐藏/显示（display：none），安全性低
v-if：赋值true/false，控制元素的dom生成/移除，安全性高，但资源消耗大
v-on：事件绑定，简写一个 @，事件绑定中默认参数event使用$event传递
            事件修饰符：.stop=stopPropagation()
                                .prevent=preventDefault()
                                .once 事件只执行一次
            键盘事件按键修饰符：         
                                .enter
                                .tab
                                .delete
                                .esc
                                .space 以及 .方向键   2.0新增 .ctrl/.shift/.alt   
v-bind：属性绑定，简写一个 ：
              绑定普通属性时，可动态控制属性参数
              当绑定class属性时，可以已对象的形式在data中设置多个class样式的true/false，同事也可以放在computed里面做逻辑操作返回。
              数组形式：在数组中直接放入class在data中的key
v-cloak：控制数据加载时页面闪动，在style中加入[v-cloak]{display：none}
v-for：列表渲染，一般需加上key属性
{{}} 不能作用在html属性中

数组的更新检测：
变异方法：数组在内存中发生实际变化，会引起视图的直接变化
                push()/pop()/shift()/unshift()/splice()/sort()/reverse()
替换数组：数组在内存中没有发生变化，会返回一个新数组，不会引起视图的变化
                filter()/concat()/slice()    

vue指令：v-model   双向数据绑定（页面动态渲染），
                1.忽略所有表单元素的特性初始值：value，checked，selected
                2.修饰符：
                    .lazy延迟渲染，减轻压力，不需要实时绑定
                    .number只有当数据为number类型时才渲染
                    .trim对绑定数据的首尾空格自动过滤 
                
vue属性：
    data（数据），methods（函数），computed（计算），watch（侦听），props（子组件接收父组件）
计算属性：
    计算属性computed：{ 方法 }，调用计算属性的方法时不加括号 
    computed与methods的区别：
       computed是基于依赖进行缓存，调用时从缓存取出之前的结果，只有当依赖发生改变时才会重新执行
       methods是没调用一次就会执行一次，从使用情况&性能优化选择两种方式
    computed与watch的区别：
        watch可以实时侦听到数据的动态变化，并做出相应的响应（可延迟操作，列如搜索请求，减轻服务器压力）。

        一般用于表单验证，其他地方使用computed
    
    computed不止是用于字面计算，所有函数中数据变化较少，单一数据变化优先考虑使用computed属性

this指向当前组件

组件结构：components.vue 文件后缀为vue
<template>试图，其中只能有一个大的根组件在template下最外层</template>
<script>
    export default{
        属性名：{}
    }
</script>
<style scoped>
    样式写入，scoped：设置为该样式只在当前组件有效
</style>

组件使用：
1.组件基本格式定义好之后，在App.vue根组件中 import 引入 该文件
2.在APP根组件的components中绑定该组件，绑定写入时使用引入时的命名
3.使用组件时在App根组件template中写入<组件命名/>

在引入组件后，组件是以元素的形式的展现的，可以说组件是一个HTML扩展元素

data属性必须是一个有返回值的函数，建议ES6写法的形式，data(){ return { key:value}}

父子组件：父组件中以组件使用的形式引入子组件
    父子组件间的通信：父 -> 子，通过props属性传递
                                  子 -> 父，通过$emit事件传递

    父组件向子组件传递数据：
    在父组件中的子元素上绑定属性，在子组件中通过props属性接收
                     形式为数组形式，["父组件中定义的属性key"]，数据绑定形式实现动态传递
    props属性：接收的key命名在父组件模板中以-分隔命名，驼峰命名无效，不区分大小写
                        props:{
                            propA: {  Number /  [String, Number]  （基础原生类型限制一个或多个，多个为数组形式，null为任何类型）
                                        required: true,  （必传）
                                        default: 值 / function(){ruturn {key:value}}, （默认值，数组/对象的默认值由函数返回）
                                        validator: function (value) { return value限制条件}（自定义验证函数）
                            }
                        }

    子组件向父组件返回数据：
    1.在子组件中绑定事件，在函数中使用this.$emit（key,value）进行传递
    2.在父组件中以key值绑定事件的类型，通过该事件接收数据（在函数写入参数，类似Ajax请求）

    父组件将数据传递给子组件，子组件使用/处理过后，返回给父组件使用
                            
    插槽： 父组件通过slot属性=key，在子组件中通过slot标签name属性=key，进行相对应插槽
                在子组件slot标签上绑定key属性，在父组件中通过slot-scope属性=key值，获取子组件向父组件传递的数据
                在2.5.0之前的版本父组件中slot相关属性要写在自定义的template元素下