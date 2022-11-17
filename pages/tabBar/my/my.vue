<template>
	<view class="container">
		<image :src="bgImageURL"
			mode="aspectFill"
			style="width: 100%; height: 100%; background-color: #ffffff;position: absolute;">
		</image>
		<view class="my-info">
			<view class="my-head">
				<u-image :src="headImageURL"
					shape="circle"></u-image>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				bgImageURL: 'https://me.heimaoba.cn/static/image/mybg.png',
				headImageURL: 'https://me.heimaoba.cn/static/image/oneqrbg.png',
			}
		},
		methods: {}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #ffffff;
		height: 100%;
	}
</style>
