<template>
	<div class="content" style="width: 66%; border: 1px solid #ccc; margin-left: 20px;">
		<a-space direction="vertical" size="large" style="width: 500px; margin: 0 auto; display: flex; justify-content: center;">
			<a-form :model="form" :layout="layout">
				<a-form-item>
					<a-space direction="vertical" style="width: 100%;">
						<a-upload action="/" :fileList="file ? [file] : []" :show-file-list="false" @change="onChange"
							@progress="onProgress">
							<template #upload-button>
								<div :class="`arco-upload-list-item${file && file.status === 'error' ? ' arco-upload-list-item-error' : ''
									}`">
									<div class="arco-upload-list-picture custom-upload-avatar" v-if="file && file.url">
										<img :src="file.url" />
										<div class="arco-upload-list-picture-mask">
											<IconEdit />
										</div>
										<a-progress v-if="file.status === 'uploading' && file.percent < 100"
											:percent="file.percent" type="circle" size="mini" style="position: absolute; left: 50%; top: 50%; transform: translateX(-50%) translateY(-50%);" />
									</div>
									<div class="arco-upload-picture-card" v-else>
										<div class="arco-upload-picture-card-text">
											<IconPlus />
											<div style="margin-top: 10px; font-weight: 600;">Upload</div>
										</div>
									</div>
								</div>
							</template>
						</a-upload>
					</a-space>
				</a-form-item>
				<a-form-item field="name" label="Username">
					<a-input v-model="form.name" placeholder="please enter your username..." />
				</a-form-item>
				<a-form-item field="descriptions" label="descriptions">
					<a-input v-model="form.description" placeholder="please enter your post..." />
				</a-form-item>
				<a-form-item field="links" label="社交媒体">
					<div>
						<div v-for="(link, index) in form.link" :key="index" style="margin-bottom: 10px;">
							<a-space>
								<a-input v-model="link.name" placeholder="请输入名称(如:Twitter)" style="width: 150px;" />
								<a-input v-model="link.url" placeholder="请输入链接地址" style="width: 275px;" />
								<a-button status="danger" @click="removeLink(link.name)">删除</a-button>
							</a-space>
						</div>
						<a-button type="outline" @click="addLink">添加社交媒体链接</a-button>
					</div>
				</a-form-item>
				<a-form-item field="btn">
					<a-button type="primary" @click="updateInfo">确认</a-button>
				</a-form-item>

			</a-form>
		</a-space>
	</div>
</template>

<script setup lang="ts">
const file = ref();
import { defineProps, reactive, ref } from 'vue';
import { FileItem, Message } from '@arco-design/web-vue';

const props = defineProps({
	userInfo: {
		type: Object,
		required: true
	}
})

function toast() {
	console.log("first")
}

const emit = defineEmits(['update'])


const layout = ref<'horizontal' | 'vertical' | 'inline'>('vertical')

interface SocialLink {
	name: string;
	url: string;
}

const form = reactive({
	avatar:'',
	name: '',
	description: '',
	link: [] as SocialLink[]
	
})

const updateInfo = () =>{
	emit('update', form)
}

const removeLink = (index:string) => {
	console.log("删除", index)
}

const canAddNewLink = (): boolean => {
	if (form.link.length === 0) return true;
	const lastLink = form.link[form.link.length - 1];
	return lastLink.name.trim() !== '' && lastLink.url.trim() !== '';
}

const addLink = () => {
	if (!canAddNewLink()) {
		Message.warning('请先完成当前链接的填写');
		return;
	}
	form.link.push({name: "", url: ""});
}

const onChange = (fileList: FileItem[], fileItem: FileItem) => {
	form.avatar = file.value?.url
	file.value = fileItem; 
};

const onProgress = (fileItem: FileItem) => {
	file.value = fileItem; 
};


</script>

<style scoped>
.content {
	width: 66%;
	border: 1px solid #ccc;
	margin-left: 20px;
}
.avatar {
    margin: auto;
}
</style>
