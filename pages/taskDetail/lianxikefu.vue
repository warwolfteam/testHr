<template>
	<view class="container">
		<view class="paixu">
			<view class="bg-set">
				<view class="wangzhi">
					<uqrcode ref="kefuCode"
						canvas-id="kefuQrcode"
						:value="qrcodeUrl"
						:options="{ margin: 20 }"
						size="190"></uqrcode>
				</view>
			</view>
			<view class="miaoshu"> 请保存该二维码 </view>
			<view class="anniu">
				<u-button type="warning"
					size="medium"
					@click="createQrCode">保存二维码</u-button>
			</view>
		</view>
	</view>
</template>
<script>
	import UQRCode from '@uqrcode/js';
	export default {
		data() {
			return {
				qrcodeUrl: "www.testhr.com",
				bgImageURL: 'https://me.heimaoba.cn/static/image/qrbg.png',
			}
		},
		mounted() {},
		methods: {
			createQrCode() {
				// uqrcode为组件的ref名称
				this.$refs.kefuCode.save({
					success: () => {
						uni.showToast({
							icon: 'success',
							title: '保存成功'
						});
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
			height: 70%;
			width: 100%;
			padding: 5%;
			text-align: center;

			.icon {
				margin: 30rpx;
			}

			.bg-set {
				background-image: url(https://me.heimaoba.cn/static/image/qrbg.png);
				background-size: 100%;
				width: 100%;
				height: 85%;
				z-index: -999;
				overflow-x: hidden;

				.wangzhi {
					width: 55%;
					height: 45%;
					margin-top: 35%;
					margin-left: 23%;
					margin-bottom: 37%;
					margin-right: 25%;
					font-size: 40rpx;
					font-weight: 1000;
				}
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
