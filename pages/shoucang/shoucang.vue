<template>
	<view class="container">
		<view class="zhiwei-body">
			<z-zhiwei-list :dataList="zZhiweiData"></z-zhiwei-list>
		</view>
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	import zZhiweiList from '@/components/z-zhiwei-list/z-zhiwei-list.vue'
	export default {
		components: {
			zZhiweiList
		},
		data() {
			return {
				zZhiweiData: homeData.zZhiweiData.data.list,
			}
		},
		methods: {}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #cccccc47;

		.zhiwei-body {
			padding: 10rpx;
			background-color: #cccccc47;
		}
	}
</style>
