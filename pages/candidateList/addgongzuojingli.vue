<template>
	<view class="container">
		<view class="bg">
			<view class="allList">
				<view class="candidate">
					<view class="candidate-jichuxinxi">
						<u-cell-group :border="false">
							<u-cell-item title="在职时间"
								hover-class="none"
								:border-top="false"
								:border-bottom="true"
								:use-label-slot="true"
								:arrow="false">
								<view class="zaizhishijian"
									slot="label">
									<view class="startTime">
										<u-input placeholder="开始时间"
											@click="openStartTime"
											v-model="startTime"
											input-align="left"
											type="text"
											:disabled="true"
											:border="false" />
									</view>
									<view class="line">
										<text>-</text>
									</view>
									<view class="endTime">
										<u-input placeholder="结束时间"
											@click="openEndTime"
											v-model="endTime"
											input-align="center"
											type="text"
											:disabled="true"
											:border="false" />
									</view>
									<view class="zhijing">
										<text @click="onzhijing">至今</text>
									</view>
								</view>
							</u-cell-item>
							<u-cell-item title="岗位名称"
								hover-class="none"
								:border-top="false"
								:border-bottom="false"
								:use-label-slot="true"
								:arrow="false">
								<u-input slot="label"
									placeholder="请输入岗位名称"
									v-model="gwName"
									input-align="left"
									type="text"
									:border="false" />
							</u-cell-item>
						</u-cell-group>
					</view>
				</view>
				<view class="gongzuojinli">
					<view class="jianliList">
						<view class="gongzuojinli-jianli">
							<view class="gongzuojinli-jianli-zhiwei">
								<span class="zhiwei"> 工作内容 </span>
							</view>
						</view>
						<u-input v-model="text"
							placeholder="请填写工作内容,控制在1000字以内"
							type="textarea"
							:border="false"
							height="500"
							maxlength="1000"
							:auto-height="true" />
					</view>
				</view>
			</view>
		</view>
		<view class="candidate-botton">
			<u-button type="warning"
				@click="onSubmit">保存</u-button>
		</view>
		<u-calendar v-model="showStartTime"
			@change="confirmStartTime"
			mode="date"></u-calendar>
		<u-calendar v-model="showEndTime"
			@change="confirmEndTime"
			mode="date"></u-calendar>
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	export default {
		components: {},
		data() {
			return {
				showStartTime: false,
				showEndTime: false,
				gwName: "",
				startTime: "",
				endTime: "",
				text: ""
			}
		},
		onLoad: function(option) {
			console.log("option:", option);
		},
		methods: {
			openStartTime() {
				console.log("点击开始时间");
				this.showStartTime = true;
			},
			openEndTime() {
				console.log("点击结束时间");
				this.showEndTime = true;
			},
			onzhijing() {
				console.log("点击至今");
				this.endTime = "至今";
			},
			confirmStartTime(e) {
				console.log("点击confirmStartTime", e);
				console.log("e.result:", e.result);
				this.startTime = e.result;
			},
			confirmEndTime(e) {
				console.log("点击confirmEndTime", e);
				console.log("e.result:", e.result);
				this.endTime = e.result;
			},
			onSubmit() {
				console.log("点击提交");
				uni.navigateBack({
					delta: 1
				});
			},
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

					.candidate-jichuxinxi {
						margin-top: 10rpx;

						.zaizhishijian {
							width: 100%;
							height: 80rpx;
							display: flex;

							.startTime {
								width: 30%;
								height: 70rpx;
								line-height: 70rpx;
								align-items: flex-start;
							}

							.line {
								height: 70rpx;
								width: 5%;
								line-height: 70rpx;
								align-items: flex-start;
								font-size: 38rpx;
							}

							.endTime {
								width: 30%;
								height: 70rpx;
								line-height: 70rpx;
								align-items: flex-start;
							}

							.zhijing {
								width: 35%;
								height: 70rpx;
								line-height: 70rpx;
								align-items: flex-end;
								text-align: right;
								color: #ff9900;
								font-weight: 1000;
							}
						}
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

						.candidate-cell-icon {
							float: right;
							height: 50rpx;
						}
					}

					.jianliList {
						padding: 30rpx;

						.gongzuojinli-jianli {
							width: 100%;
							height: 90rpx;
							margin-top: 10rpx;
							margin-bottom: 10rpx;

							// padding-left: 25rpx;
							// padding-right: 25rpx;
							.gongzuojinli-jianli-zhiwei {
								float: left;
								display: flex;

								.zhiwei {
									align-items: center;
									font-size: 29rpx;
									font-weight: 1000;
									color: #181818;
								}
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
			z-index: 999;
			width: 100%;
			background-color: #fff;
			position: fixed;
			bottom: 0;
			padding-top: 30rpx;
			padding-bottom: 30rpx;
			padding-left: 30rpx;
			padding-right: 30rpx;
		}
	}
</style>
