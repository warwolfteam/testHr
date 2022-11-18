<template>
	<view class="container">
		<image class="bg-set"
			:src="bgImageURL"></image>
		<view class="content">
			<view class="my-info"
				@click="onInfo">
				<view class="my-info-left">
					<view class="my-info-head">
						<u-image :src="headImageURL"
							width="100rpx"
							height="100rpx"
							shape="circle"></u-image>
					</view>
					<view class="my-info-xinxi">
						<view class="my-info-xinxi-name"> 曾老师 </view>
						<view class="my-info-xinxi-company"> 江西七善科技有限公司 </view>
					</view>
				</view>
				<view class="my-info-right">
					<view class="my-info-jiantou">
						<u-icon class="sIcon"
							@click="onInfo"
							name="arrow-right"
							color="#ffffff"
							size="30"></u-icon>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				bgImageURL: 'https://me.heimaoba.cn/static/image/mybg.png',
				headImageURL: 'https://me.heimaoba.cn/static/image/defaultCompany.png',
			}
		},
		methods: {
			onInfo() {
				console.log("点击箭头");
			}
		}
	}
</script>
<style>
	/*要设置的body样式设置在这里面*/
	page {
		background-image: url(https://me.heimaoba.cn/static/image/mybg.png);
		background-size: 100%;
		width: 100%;
		height: 100%;
		z-index: -999;
	}
</style>
<style lang="scss"
	scoped>
	.bg-set {
		position: fixed;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		z-index: -1;
	}

	.content {
		z-index: 100;

		.my-info {
			margin-top: 150rpx;
			height: 200rpx;
			// background: #000;
			width: 100%;
			padding: 50rpx;

			.my-info-left {
				float: left;
				display: flex;
				width: 70%;

				.my-info-head {
					align-items: center;
					// float: left;
				}

				.my-info-xinxi {
					align-items: center;
					margin-left: 20rpx;
					height: 120rpx;

					.my-info-xinxi-name {
						height: 40rpx;
						color: #fff;
						font-size: 40rpx;
						font-weight: 1000;
					}

					.my-info-xinxi-company {
						margin-top: 20rpx;
						height: 38rpx;
						color: #fff;
					}
				}
			}

			.my-info-right {
				width: 18%;
				float: right;

				.my-info-jiantou {
					float: right;
					margin-top: 25rpx;
					margin-left: 25rpx;
				}
			}
		}
	}
</style>
