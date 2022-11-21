<template>
	<view class="container">
		<view class="paixu">
			<view class="wangzhi"> {{qrcodeUrl}} </view>
			<view class="miaoshu"> 请保存该二维码 </view>
			<view class="anniu">
				<u-button type="warning"
					size="medium"
					@click="copy">保存二维码</u-button>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				qrcodeUrl: "www.testhr.com"
			}
		},
		methods: {
			copy() {
				uni.setClipboardData({
					data: this.qrcodeUrl,
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
