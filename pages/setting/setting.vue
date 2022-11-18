<template>
	<view class="container">
		<view class="my-setting">
			<u-cell-group>
				<u-cell-item title="登录手机号"
					value="139******66"></u-cell-item>
			</u-cell-group>
		</view>
		<view class="my-botton">
			<u-button type="error">退出登录</u-button>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {}
		},
		methods: {}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #ffffff47;
		height: 100vh;

		.my-setting {
			margin-top: 30rpx;
		}

		.my-botton {
			bottom: 30rpx;
			margin-top: 600rpx;
			margin-bottom: 100rpx;
			margin-left: 100rpx;
			margin-right: 100rpx;
		}
	}
</style>
