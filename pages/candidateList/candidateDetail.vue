<template>
	<view class="container">
		<view class="bg">
			<!-- 候选人详情 -->
			<view class="allList">
				<view class="candidate">
					<view class="candidate-cell">
						<view class="candidate-cell-name">
							<span class="userName">李四</span>
							<span class="sexIcon">
								<i class="iconfont icon-nvxing"></i>
							</span>
						</view>
						<view class="candidate-cell-status"> 新添加 </view>
					</view>
					<view class="candidate-miaosu">
						<view class="candidate-miaosu-xinxi">
							<span class="xinxi">男 | 31岁 | 大专</span>
						</view>
						<view class="candidate-miaosu-time"> 2天前 </view>
					</view>
					<view class="candidate-mianshi">
						<view class="candidate-mianshi-shijian">
							<span class="xinxi">期望面试时间：</span>
							<span class="xinxi">{{mianshiTime}}</span>
						</view>
						<view class="candidate-mianshi-edit">
							<u-icon name="edit-pen"
								color="#00ff00"
								size="28"
								@click="editMianShi"></u-icon>
						</view>
					</view>
					<view class="candidate-jichuxinxi">
						<u-cell-group :border="false">
							<u-cell-item title="手机号"
								:border-top="false"
								:border-bottom="true"
								:arrow="false"
								@click="callPhone">
								<view slot="right-icon">
									{{phone}}
									<u-icon size="26"
										name="phone"></u-icon>
								</view>
							</u-cell-item>
							<u-cell-item title="专业"
								hover-class="none"
								:value="zhuangye"
								:border-top="false"
								:border-bottom="true"
								:arrow="false">
							</u-cell-item>
							<u-cell-item title="毕业时间"
								hover-class="none"
								:value="biyeTime"
								:border-top="false"
								:border-bottom="true"
								:arrow="false">
							</u-cell-item>
							<u-cell-item title="现居住地"
								hover-class="none"
								:value="juzhidizhi"
								:border-top="false"
								:border-bottom="false"
								:arrow="false">
							</u-cell-item>
						</u-cell-group>
					</view>
				</view>
				<view class="gongzuojinli">
					<view class="gongzuojinli-cell">
						<view class="candidate-cell-name">
							<span class="userName">工作经历</span>
						</view>
					</view>
					<view class="jianliList"
						v-for="(item, index)  in gzjlList"
						:key="index">
						<view class="gongzuojinli-jianli">
							<view class="gongzuojinli-jianli-zhiwei">
								<span class="zhiwei"> {{item.zhiwei}}</span>
							</view>
							<view class="gongzuojinli-jianli-time"> {{item.time}} </view>
						</view>
						<view class="text-box"
							scroll-y="true">
							<text>{{item.text}}</text>
						</view>
					</view>
				</view>
			</view>
		</view>
		<u-popup v-model="show"
			mode="bottom"
			height="25%"
			border-radius="14">
			<view class="qiwang">
				<view class="qiwang-input">
					<u-input v-model="mianshiTime"
						type="textarea"
						:border="true"
						height="200"
						:auto-height="true" />
				</view>
				<view class="qiwang-bottom">
					<u-button size="mini"
						type="warning"
						@click="onMianShi">确定</u-button>
				</view>
			</view>
			<!-- <u-field v-model="mobile"
				:border-bottom="false"
				placeholder="请填写期望面试时间"
				type="textarea">
				<u-button size="mini"
					slot="right"
					type="warning"
					@click="onMianShi">确定</u-button>
			</u-field> -->
		</u-popup>
		<view class="candidate-botton">
			<u-button type="warning">编辑候选人信息</u-button>
		</view>
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	export default {
		components: {},
		data() {
			return {
				show: false,
				phone: "13989898556",
				zhuangye: "--",
				biyeTime: "--",
				juzhidizhi: "--",
				mianshiTime: "下午三点",
				gzjlList: [{
					id: "0",
					time: "2014.11-2022.10",
					zhiwei: "客服",
					text: "客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服客服"
				}, {
					id: "1",
					time: "2014.11-2022.10",
					zhiwei: "前台",
					text: "前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台"
				}, {
					id: "2",
					time: "2014.11-2022.10",
					zhiwei: "前台",
					text: "前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台前台"
				}]
			}
		},
		onLoad: function(option) {
			console.log("option:", option);
		},
		methods: {
			callPhone() {
				console.log("点击手机号");
				uni.makePhoneCall({
					phoneNumber: this.phone //仅为示例
				});
			},
			editMianShi() {
				console.log("点击修改图标");
				this.show = true;
			},
			onMianShi() {
				console.log("填写期望面试时间");
				this.show = false;
			}
		}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #a2a2a247;
		width: 100%;

		// height: 100vh;
		.select {
			background-color: #ffffff;
			margin-bottom: 20rpx;
		}

		.bg {
			// background-color: #e7e7e7;
			padding-top: 30rpx;
			padding-bottom: 30rpx;

			.allList {
				.candidate {
					// height: 180rpx;
					background-color: #ffffff;
					padding: 30rpx;
					margin-bottom: 20rpx;
					margin-left: 20rpx;
					margin-right: 20rpx;
					border-radius: 18rpx;

					.candidate-cell {
						width: 100%;
						height: 60rpx;
						margin-top: 10rpx;
						margin-bottom: 10rpx;
						padding-left: 25rpx;
						padding-right: 25rpx;

						.candidate-cell-name {
							float: left;
							display: flex;
							height: 50rpx;

							.userName {
								height: 50rpx;
								line-height: 50rpx;
								align-items: center;
								margin-right: 20rpx;
								font-size: 38rpx;
								font-weight: 1000;
							}

							.sexIcon {
								height: 50rpx;
								line-height: 50rpx;
								align-items: center;
								font-size: 18rpx;
								color: #0055ff;
							}
						}

						.candidate-cell-status {
							float: right;
						}
					}

					.candidate-miaosu {
						width: 100%;
						height: 50rpx;
						margin-top: 10rpx;
						margin-bottom: 10rpx;
						padding-left: 25rpx;
						padding-right: 25rpx;

						.candidate-miaosu-xinxi {
							float: left;
							display: flex;

							.xinxi {
								align-items: center;
								font-size: 24rpx;
								color: #717171;
							}
						}

						.candidate-miaosu-time {
							float: right;
							font-size: 24rpx;
							color: #717171;
						}
					}

					.candidate-mianshi {
						width: 100%;
						height: 50rpx;
						margin-top: 10rpx;
						margin-bottom: 10rpx;
						padding-left: 25rpx;
						padding-right: 25rpx;

						.candidate-mianshi-shijian {
							float: left;
							display: flex;

							.xinxi {
								align-items: center;
								font-size: 24rpx;
								color: #9d9d9d;
							}
						}

						.candidate-mianshi-edit {
							float: right;
							font-size: 24rpx;
							color: #717171;
						}
					}

					.candidate-jichuxinxi {
						margin-top: 10rpx;
					}
				}

				.gongzuojinli {
					// height: 180rpx;
					background-color: #ffffff;
					padding: 30rpx;
					margin-bottom: 100rpx;
					margin-left: 20rpx;
					margin-right: 20rpx;
					border-radius: 18rpx;

					.gongzuojinli-cell {
						width: 100%;
						height: 60rpx;
						margin-top: 10rpx;
						margin-bottom: 10rpx;
						padding-left: 25rpx;
						padding-right: 25rpx;

						.candidate-cell-name {
							float: left;
							display: flex;
							height: 50rpx;

							.userName {
								height: 50rpx;
								line-height: 50rpx;
								align-items: center;
								margin-right: 20rpx;
								font-size: 38rpx;
								font-weight: 1000;
							}
						}
					}

					.jianliList {
						padding: 30rpx;

						.gongzuojinli-jianli {
							width: 100%;
							height: 50rpx;
							margin-top: 30rpx;
							margin-bottom: 10rpx;

							// padding-left: 25rpx;
							// padding-right: 25rpx;
							.gongzuojinli-jianli-zhiwei {
								float: left;
								display: flex;

								.zhiwei {
									align-items: center;
									font-size: 34rpx;
									font-weight: 1000;
									color: #181818;
								}
							}

							.gongzuojinli-jianli-time {
								float: right;
								font-size: 24rpx;
								color: #979797;
							}
						}
					}
				}
			}

			.candidate-bottom {
				background-color: #fff;
			}

			.kong {
				width: 100%;
				height: 50vh;
				// background-color: #dedede;
			}
		}

		.candidate-botton {
			width: 100%;
			background-color: #fff;
			position: fixed;
			bottom: 0;
			padding-top: 10rpx;
			padding-bottom: 10rpx;
			padding-left: 30rpx;
			padding-right: 30rpx;
		}

		.qiwang {
			padding: 30rpx;
			display: flex;

			.qiwang-input {
				width: 90%;
				align-items: center;
			}

			.qiwang-bottom {
				align-items: center;
				margin-left: 30rpx;
				padding-top: 14%;
			}
		}
	}
</style>
