<template>
	<view class="container">
		<image :src="bgImageURL"
			mode="aspectFit"
			style="width: 100%; height: 100%; background-color: #ffffff;position: absolute;">
		</image>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				bgImageURL: 'https://me.heimaoba.cn/static/image/oneqrbg.png',
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
