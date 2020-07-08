<template>
	<view>
		<u-form-item :label="label" :prop="prop">
			<u-input v-model="showValue" type="select" @click="show=true" :select-open="show" />
		</u-form-item>
		<u-select v-model="show" :list="list" :default-value="defaultVal" @confirm="selectConfirm"></u-select>
	</view>
</template>

<script>
	export default {
		props: {
			list: Array,
			label: String,
			value: [Number, String],
			prop: String,
			defaultValue: ''
		},
		data() {
			return {
				showValue: '',
				show: false,
				defaultVal: [0]

			};
		},
		methods: {
			selectConfirm(e) {
				//console.log(e);
				this.showValue = e[0]['label']
				this.$emit('input', e[0]['value'])
				//选择后把默认值设为当前选择的
				for (let i = 0; i < this.list.length; i++) {
					if (this.list[i]['value'] == e[0]['value']) {
						this.defaultVal = [i];
						return;
					}
				}
			}
		},
		mounted() {
			//console.log(this.list);
			//初始化显示默认值
			for (let i = 0; i < this.list.length; i++) {
				if (this.list[i]['value'] == this.defaultValue) {
					this.showValue = this.list[i]['label'];
					this.defaultVal = [i];
					return;
				}
			}
		}
	}
</script>

<style>

</style>
