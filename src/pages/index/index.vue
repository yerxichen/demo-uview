<template>
	<view class="content">
		<u-form :model="form" ref="uForm">
			<u-form-item label="姓名" prop="name">
				<u-input v-model="form.name" />
			</u-form-item>
			<dic-select v-model="form.gj" :list="gjList" label="国家" defaultValue="002"></dic-select>
			<dic-select v-model="form.xb" :list="xbList" label="性别" defaultValue="0"></dic-select>
		</u-form>
		<u-form-item label="上传文件" label-position="top">
			<u-upload :action="action" :file-list="fileList"></u-upload>
		</u-form-item>
		
		<u-button type="primary" @click="tj">提交</u-button>
		<u-button type="success" @click="tjHttp">测试http</u-button>
	</view>
</template>

<script>
	import dicSelect from '../../components/dic-select.vue'
	export default {
		components: {
			dicSelect
		},
		data() {
			return {
				title: 'Hello',
				show: false,
				gjList: [{
					value: '001',
					label: '中国'
				}, {
					value: '002',
					label: '日本'
				}],
				xbList: [{
					value: '0',
					label: '男'
				}, {
					value: '1',
					label: '女'
				}],
				form: {
					name: '',
					xb: '0',
					gj: '1'
				},

				rules: {
					name: [
						// 对name字段进行必填验证
						{
							required: true,
							message: '请填写姓名',
							trigger: ['change', 'blur']
						},
					],
					xb: [
						// 对name字段进行必填验证
						{
							required: true,
							message: '请填写性别',
							trigger: ['change', 'blur']
						},
					]
				},
				// 演示地址，请勿直接使用
				action: 'http://localhost:18081/upload/fileUpload',
				fileList: [{
					url: 'http://pics.sc.chinaz.com/files/pic/pic9/201912/hpic1886.jpg',
				}]
			}
		},
		onLoad() {

		},
		methods: {
			showSelect() {
				this.show = true
			},
			selectConfirm(e) {
				console.log(e);
				// alert(e[0]['label'])
				this.form.xb = e[0]['value']
				this.formmc.xbmc = e[0]['label']
			},
			tj() {
				console.log(this.form);
				this.$refs.uForm.validate(valid => {
					if (valid) {
						console.log('验证通过');
					} else {
						console.log('验证失败');
					}
				});
			},
			async tjHttp(){
				let result=await this.$u.get("/user/getUserList");
				console.log(result);
			}
		
		},
		onReady() {
			this.$refs.uForm.setRules(this.rules);
		}
	}
</script>

<style>
	.content {
		padding: 20rpx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
