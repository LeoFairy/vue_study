<template>
   <!--  组件结构 -->
    <div >
      <h2>学生名称：{{name}} </h2>
      <h2>学生年龄：{{age}}</h2>
    </div>
</template>

<script>
  // 组件交互相关代码（数据、方法）
    export default {
    name:'Student',
    data() {
      return {
        name: "vue",
        age: "18",
      };
    },
  }
</script>