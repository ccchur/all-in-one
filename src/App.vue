
<template>
  <div class="container">
    <Card :userInfo="userInfo" />
    <Content :userInfo="userInfo" @update="update" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import Card from './components/Card.vue';
import Content from './components/Content.vue';
import { Descriptions } from '@arco-design/web-vue';



const userInfo = ref({
  avatar: "https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp",
  name: "张三",
  description: "我是一个前端工程师",
  link: [
    {
      id: 1,
      icon: "icon-github",
      text: "Github",
      link: "https://github.com/zhangyuang"
    },
    {
      id: 2,
      icon: "icon-twitter",
      text: "Twitter",
      link: "https://twitter.com/zhangyuang"
    },
    {
      id: 3,
      icon: "icon-linkedin",
      text: "Linkedin",
      link: "https://www.linkedin.com/in/zhangyuang/"
    }
  ]
})

const update = (e:string) => {
  console.log("first",e)
}

</script>
<style scoped>
.container {
  width: 100%;
  display: flex;
  justify-content: space-around;
}
</style>