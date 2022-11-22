<template>
	<view class="container">
		<view class="bg">
			<view class="myinfo">
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item :title="zhiwuName"
							:title-style="headTittleStyle"
							:border-top="false"
							:border-bottom="false"
							:arrow="false"></u-cell-item>
					</u-cell-group>
				</view>
			</view>
			<view class="myinfo">
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item title="需求人数"
							hover-class="none"
							:border-top="false"
							:border-bottom="true"
							:arrow="false">
							<view slot="right-icon"
								class="renshu">
								{{jiedanNumber}}人
							</view>
						</u-cell-item>
						<u-cell-item title="接单人数"
							hover-class="none"
							:border-top="false"
							:border-bottom="false"
							:arrow="false">
							<view slot="right-icon"
								class="renshu">
								{{renshu}}人
							</view>
						</u-cell-item>
					</u-cell-group>
				</view>
			</view>
			<view class="myinfo">
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item title="结算方式"
							hover-class="none"
							:border-top="false"
							:border-bottom="true"
							:arrow="false">
							<view slot="right-icon"
								class="renshu">
								{{jiesuanType}}
							</view>
						</u-cell-item>
						<u-cell-item title="价格类型"
							hover-class="none"
							:border-top="false"
							:border-bottom="true"
							:arrow="false">
							<view slot="right-icon"
								class="jiageleixin">
								<view class="jiageleixin-top"> 服务费 </view>
								<view class="jiageleixin-bottom"> 仅包含渠道服务费 </view>
							</view>
						</u-cell-item>
						<u-cell-item hover-class="none"
							:border-top="false"
							:border-bottom="false"
							:arrow="false">
							<view slot="title"
								class="jiage-title">
								<uni-tooltip content="此价格为系统根据您的接单人数预估，请以平台实际确认为准">
									<span class="jiage-title-zi">结算价格</span>
									<span class="jiage-title-tu">
										<u-icon name="error-circle"
											color="#ee9f00"
											margin-left="20rpx"
											size="26">
										</u-icon>
									</span>
								</uni-tooltip>
							</view>
							<view slot="label"
								class="jiage-label"> 本结算价格为含税价格，结算时将扣除税费后与您进行结算 </view>
							<view slot="right-icon"
								class="jiage">
								<span class="jiage-jiesuanMoney">{{jiesuanMoney}}元</span>/人/小时
							</view>
						</u-cell-item>
					</u-cell-group>
				</view>
			</view>
		</view>
		<view class="jiedan-botton">
			<u-button type="warning"
				@click="onSubmit">立即接单</u-button>
		</view>
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	export default {
		components: {},
		data() {
			return {
				headTittleStyle: {
					'font-size': '44rpx',
					'font-weight': '1000',
					'color': '#000'
				},
				zhiwuName: "电销客服",
				jiedanNumber: 20,
				renshu: 20,
				jiesuanType: "一次性返",
				jiesuanIf: "到岗+质保3天",
				jiesuanMoney: "***",
				jiedanTime: "2022-11-14 21:55",
				id: "1"
			}
		},
		onLoad: function(option) {
			console.log("option:", option);
			this.zhiwuName = option.name;
			this.jiesuanType = option.fanxian;
			this.renshu = option.renshu;
			this.jiedanNumber = option.peopleNumber;
			this.jiesuanMoney = option.fanYongMoney;
		},
		methods: {
			onSubmit() {
				uni.switchTab({
					url: "/pages/tabBar/order/order"
				});
				console.log("去订单页");
			}
		}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #a2a2a247;
		width: 100%;
		height: 100vh;

		.jiedan-botton {
			z-index: 999;
			width: 100%;
			background-color: #fff;
			position: fixed;
			bottom: 0;
			padding-top: 30rpx;
			padding-bottom: 90rpx;
			padding-left: 30rpx;
			padding-right: 30rpx;
		}

		.bg {
			// background-color: #e7e7e7;
			padding-top: 20rpx;
			padding-bottom: 30rpx;

			.myinfo {
				background-color: #ffffff;
				padding: 20rpx;
				margin-bottom: 20rpx;
				margin-left: 10rpx;
				margin-right: 10rpx;
				border-radius: 18rpx;

				.myinfo-tittle {
					margin-left: 30rpx;
					font-size: 38rpx;
					font-weight: 1000;
				}

				.myinfo-cell {
					margin-top: 20rpx;

					.renshu {
						color: #000;
					}

					.jiageleixin {
						height: 80rpx;

						.jiageleixin-top {
							text-align: right;
							height: 50rpx;
							line-height: 50rpx;
							font-size: 35rpx;
							font-weight: 1000;
							color: #2d2d2d;
						}

						.jiageleixin-bottom {
							text-align: right;
							height: 20rpx;
							line-height: 20rpx;
							font-size: 15rpx;
							color: #919191;
						}
					}

					.jiage-title {
						width: 180rpx;
						height: 60rpx;

						.jiage-title-zi {
							margin-right: 10rpx;
							height: 58rpx;
							line-height: 58rpx;
						}

						.jiage-title-tu {
							height: 58rpx;
							line-height: 58rpx;
						}
					}

					.jiage-label {
						font-size: 18rpx;
						color: #8b8b8b;
						padding-right: 10rpx;
					}

					.jiage {
						color: #000;
						width: 180rpx;
						margin-left: 30rpx;

						.jiage-jiesuanMoney {
							font-size: 38rpx;
							color: #ff641c;
							font-weight: 1000;
							padding-right: 10rpx;
						}
					}
				}
			}
		}
	}
</style>
