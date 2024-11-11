
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

export interface UserInfo {
	avatar: string;
	name: string; 
	description: string;
	link: {
		id: number;
		icon?: string;
		name: string;
		url: string;
	}[];
}

const userInfo = ref<UserInfo>({
	avatar: "https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp",
	name: "示例数据",
	description: "我是一个前端工程师",
	link: [
		{
			id: 1,
			// icon: "icon-github", 
			name: "Github",
			url: "https://github.com/zhangyuang"
		}
	]
})

const update = (e:UserInfo) => {
	console.log("first", e);
	userInfo.value = Object.assign({},e)
}

</script>
<style scoped>
.container {
	width: 100%;
	display: flex;
	justify-content: space-around;
}
</style>
