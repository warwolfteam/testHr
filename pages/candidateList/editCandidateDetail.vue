<template>
	<view class="container">
		<view class="bg">
			<view class="candidate-cell">
				<view class="candidate-cell-name">
					<span class="userName">基本信息</span>
				</view>
			</view>
			<!-- 候选人详情 -->
			<view class="allList">
				<view class="candidate">
					<view class="candidate-jichuxinxi">
						<u-cell-group :border="false">
							<u-cell-item title="姓名"
								:border-top="false"
								:border-bottom="true"
								:use-label-slot="true"
								:arrow="false">
								<u-input slot="label"
									placeholder="请输入姓名"
									v-model="username"
									input-align="left"
									type="text"
									:border="false" />
							</u-cell-item>
							<u-cell-item title="手机号"
								:border-top="false"
								:border-bottom="true"
								:use-label-slot="true"
								:arrow="false">
								<u-input slot="label"
									placeholder="请输入手机号"
									v-model="phone"
									input-align="left"
									type="text"
									:border="false" />
							</u-cell-item>
							<u-cell-item title="身份证号"
								:border-top="false"
								:border-bottom="true"
								:use-label-slot="true"
								:arrow="false">
								<u-input slot="label"
									placeholder="请输入身份证号"
									v-model="idCardNumber"
									input-align="left"
									type="text"
									:border="false" />
							</u-cell-item>
							<u-cell-item title="性别"
								:border-top="false"
								:border-bottom="true"
								:label="sex"
								:arrow="true">
							</u-cell-item>
							<u-cell-item title="年龄"
								:border-top="false"
								:border-bottom="true"
								:use-label-slot="true"
								:arrow="false">
								<u-input slot="label"
									placeholder="请输入年龄"
									v-model="year"
									input-align="left"
									type="text"
									:border="false" />
							</u-cell-item>
							<u-cell-item title="专业"
								:border-top="false"
								:border-bottom="true"
								:use-label-slot="true"
								:arrow="false">
								<u-input slot="label"
									placeholder="请输入专业(选填)"
									v-model="zhuangye"
									input-align="left"
									type="text"
									:border="false" />
							</u-cell-item>
							<u-cell-item title="毕业时间"
								:border-top="false"
								:border-bottom="true"
								:label="biyeTime"
								:arrow="true">
							</u-cell-item>
							<u-cell-item title="现居住地"
								:border-top="false"
								:border-bottom="true"
								:label="juzhidizhi"
								:arrow="true">
							</u-cell-item>
							<u-cell-item title="详细地址"
								:border-top="false"
								:border-bottom="true"
								:use-label-slot="true"
								:arrow="false">
								<u-input slot="label"
									placeholder="请输入详细地址(选填)"
									v-model="xiangxidizhi"
									input-align="left"
									type="text"
									:border="false" />
							</u-cell-item>
							<u-cell-item title="期望面试时间"
								:border-top="false"
								:border-bottom="true"
								:use-label-slot="true"
								:arrow="false">
								<u-input slot="label"
									placeholder="请输入期望面试时间(选填)"
									v-model="mianshiTime"
									input-align="left"
									type="text"
									:border="false" />
							</u-cell-item>
						</u-cell-group>
					</view>
				</view>
				<view class="gongzuojinli">
					<view class="gongzuojinli-cell">
						<view class="candidate-cell-name">
							<span class="userName">工作经历</span>
						</view>
						<view class="candidate-cell-icon">
							<u-icon name="plus-circle"
								color="#5e5f64"
								size="40"></u-icon>
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
		<view class="candidate-botton">
			<u-button type="warning"
				@click="onSubmit">提交</u-button>
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
				username: "李四",
				phone: "13989898556",
				idCardNumber: "",
				sex: "请选择性别",
				year: "",
				zhuangye: "",
				biyeTime: "请选择毕业时间（选填）",
				juzhidizhi: "请输入现居住地（选填）",
				xiangxidizhi: "",
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
			},
			onSubmit() {
				console.log("点击编辑候选人信息");
				uni.navigateBack({
					delta: 1
				});
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
				}
			}

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
