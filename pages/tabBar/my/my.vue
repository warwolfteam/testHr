<template>
	<view class="container">
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
							name="arrow-right"
							color="#ffffff"
							size="30"></u-icon>
					</view>
				</view>
			</view>
			<!-- 任务返佣信息 -->
			<view class="my-yongjing">
				<view class="fanyong-head">
					<view class="fanyong-tittle">
						<u-icon name="question-circle"
							color="#000000"
							size="40"></u-icon>
						<span class="fanyong-tittle-zi">我的佣金</span>
					</view>
					<view class="fanyong-botton">
						<u-button @click="onjiesuan"
							type="warning"
							size="mini"
							:plain="true">
							<u-icon name="order"
								color="#ee9f00"
								size="25"></u-icon>结算管理
						</u-button>
					</view>
				</view>
				<view class="fanyong-xinxi"
					:style="{backgroundImage:                             
				        'url('+yjImageURL+')'}">
					<view class="my-yongjing-line">
						<u-line color="#9e9e9e" />
					</view>
					<view class="fanyong-jiesuan">
						<view class="fanyong-xinxi-tittle"> 已结算 </view>
						<view class="fanyong-xinxi-money"> ￥0.00 </view>
					</view>
					<view class="fanyong-jiesuan">
						<view class="fanyong-xinxi-tittle"> 结算中 </view>
						<view class="fanyong-xinxi-money"> ￥0.00 </view>
					</view>
				</view>
			</view>
			<view class="my-list">
				<view class="my-list-kuai">
					<u-cell-group :border="false">
						<u-cell-item icon="star"
							@click="toshoucang"
							:border-bottom="true"
							:border-top="false"
							title="我的收藏"></u-cell-item>
						<u-cell-item icon="bookmark"
							@click="tohelp"
							:border-bottom="true"
							:border-top="false"
							title="帮助中心"></u-cell-item>
						<u-cell-item icon="kefu-ermai"
							@click="callkefu"
							title="联系客服"
							value="工作日09:00-18:00"
							:border-bottom="true"
							:border-top="false">
						</u-cell-item>
						<u-cell-item icon="error-circle"
							@click="toabout"
							:border-bottom="true"
							:border-top="false"
							title="关于平台"></u-cell-item>
						<u-cell-item icon="setting-fill"
							@click="tosetting"
							:border-bottom="false"
							:border-top="false"
							title="设置"></u-cell-item>
					</u-cell-group>
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
				yjImageURL: 'https://me.heimaoba.cn/static/image/myCommission.png',
			}
		},
		methods: {
			onInfo() {
				console.log("点击我的信息");
				uni.navigateTo({
					url: "/pages/myinfo/myinfo"
				})
			},
			onjiesuan() {
				console.log("点击结算管理");
				uni.navigateTo({
					url: "/pages/jiesuan/jiesuan"
				})
			},
			callkefu() {
				console.log("点击联系客服");
				uni.makePhoneCall({
					phoneNumber: '021-1234567' //仅为示例
				});
			},
			toshoucang() {
				console.log("点击我的收藏");
				uni.navigateTo({
					url: "/pages/shoucang/shoucang"
				})
			},
			toabout() {
				console.log("点击关于平台");
				uni.navigateTo({
					url: "/pages/about/about"
				})
			},
			tosetting() {
				console.log("点击设置");
				uni.navigateTo({
					url: "/pages/setting/setting"
				})
			},
			tohelp() {
				console.log("点击帮助中心");
				uni.navigateTo({
					url: "/pages/help/help"
				})
			}
		}
	}
</script>
<!-- <style>
	/*要设置的body样式设置在这里面*/
	page {
		background-image: url(https://me.heimaoba.cn/static/image/mybg.png);
		background-size: 100%;
		width: 100%;
		height: 100%;
		z-index: -999;
	}
</style> -->
<style lang="scss"
	scoped>
	.container {
		background-image: url(https://me.heimaoba.cn/static/image/mybg.png);
		background-size: 100%;
		width: 100%;
		height: 100%;
		z-index: -999;
		overflow-x: hidden;

		.content {
			z-index: 100;
			padding-top: 150rpx;
			width: 100%;

			.my-info {
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

			.my-yongjing {
				margin-bottom: 20rpx;
				margin-left: 20rpx;
				margin-right: 20rpx;
				margin-top: 30rpx;
				height: 360rpx;
				background-color: #fff;
				border-radius: 15px;

				.fanyong-head {
					width: 100%;

					.fanyong-tittle {
						height: 50rpx;
						font-size: 25px;
						font-weight: 100;
						margin-top: 30rpx;
						padding-left: 20rpx;
						float: left;
					}

					.fanyong-botton {
						float: right;
						height: 50rpx;
						margin-top: 30rpx;
						padding-right: 20rpx;

						.fanyong-botton-zi {
							margin-left: 20rpx;
						}
					}
				}

				.fanyong-xinxi {
					float: left;
					height: 300rpx;
					width: 100%;
					padding-top: 10rpx;

					.my-yongjing-line {
						padding: 20rpx;
					}

					.fanyong-jiesuan {
						float: left;
						height: 100rpx;
						width: 100%;
						padding-top: 10rpx;

						.fanyong-xinxi-tittle {
							margin-left: 50rpx;
							font-weight: 10;
							font-size: 28rpx;
							color: #666666;
							float: left;
							width: 100%;
						}

						.fanyong-xinxi-money {
							margin-top: 10rpx;
							margin-left: 30rpx;
							font-weight: 1000;
							font-size: 38rpx;
							color: #000000;
							float: left;
							width: 100%;
						}
					}
				}
			}

			.my-list {
				margin-bottom: 120rpx;
				margin-left: 20rpx;
				margin-right: 20rpx;
				margin-top: 20rpx;
				height: 580rpx;
				background-color: #fff;
				border-radius: 15px;

				.my-list-kuai {
					padding-top: 30rpx;
				}
			}
		}
	}
</style>
