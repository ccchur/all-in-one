<template>
	<div class="content">


		<a-space direction="vertical" size="large" :style="{ width: '100%', 'align-items': 'center', margin: 'auto' }">
			<a-form :model="form" :layout="layout">
				<a-form-item>
					<a-avatar @click="toast" :size="88" class="avatar" :style="{ backgroundColor: '#FFC72E' }">
                    <img alt="avatar" :src="props.userInfo?.avatar" />
                        <IconUser />
                        <template #trigger-icon>
                        <IconEdit />
                    </template>
                </a-avatar>
			    </a-form-item>
			<a-form-item field="name" label="Username">
				<a-input v-model="form.name" placeholder="please enter your username..." />
			</a-form-item>
			<a-form-item field="post" label="Post">
				<a-input v-model="form.post" placeholder="please enter your post..." />
			</a-form-item>
			</a-form>
		</a-space>
	</div>
</template>

<script setup lang="ts">
import { defineProps, reactive, ref } from 'vue';

const props = defineProps({
	userInfo: {
		type: Object,
		required: true
	}
})

function toast() {
	// this.$message.info('Uploading...');
	console.log("first")
}

const emit = defineEmits(['update'])

const updateInfo = () => {
	emit('update', '修改')
}

const layout = ref<'horizontal' | 'vertical' | 'inline'>('vertical')

const form = reactive({
	name: '',
	post: '',
	isRead: false,
})


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
