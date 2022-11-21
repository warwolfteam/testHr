<template>
	<view class="container">
		<view class="paixu">
			<view class="icon">
				<u-icon name="zhuanfa"
					color="#2979ff"
					size="128"></u-icon>
			</view>
			<view class="wangzhi"> {{wangzhi}} </view>
			<view class="miaoshu"> 请使用电脑打开网页版操作 </view>
			<view class="anniu">
				<u-button type="warning"
					size="medium"
					@click="copy">复制网址</u-button>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				wangzhi: "www.testhr.com"
			}
		},
		methods: {
			copy() {
				uni.setClipboardData({
					data: this.wangzhi,
					success: function() {
						console.log('success');
					}
				});
			}
		}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #ffffff;
		height: 100vh;

		.paixu {
			padding-top: 25%;
			height: 60%;
			width: 100%;
			padding: 20%;
			text-align: center;

			.icon {
				margin: 30rpx;
			}

			.wangzhi {
				margin-top: 20rpx;
				font-size: 40rpx;
				font-weight: 1000;
			}

			.miaoshu {
				margin-top: 20rpx;
			}

			.anniu {
				margin-top: 40rpx;
			}
		}
	}
</style>
