<template>
   <!--  组件结构 -->
    <div class="demo">
      <h2>学校名称：{{name}} </h2>
      <h2>学校地址：{{address}}</h2>
      <button @click="showName">点我提示学校名</button>
    </div>
</template>

<script>
  // 组件交互相关代码（数据、方法）
    export default {
    name:'School',
    data() {
      return {
        name: "vue",
        address: "北京",
      };
    },
    methods: {
      showName() {
        console.log("showName", this);
      },
    },
  }

</script>

<style> 
 /*  组件的样式 */
  .demo{
    background-color: orange;
  }
</style>