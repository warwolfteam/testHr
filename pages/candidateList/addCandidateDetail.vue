<template>
	<view class="container">
		<view class="bg">
			<view class="zhantie">
				<view class="zhantie-input">
					<u-input v-model="text"
						:placeholder="zhantieText"
						type="textarea"
						:border="true"
						height="200"
						maxlength="1000"
						:auto-height="true" />
				</view>
				<view class="zhantie-button">
					<u-button type="warning"
						size="mini"
						@click="shibie">识别</u-button>
				</view>
			</view>
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
								:arrow="true"
								@click="selectSex">
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
							<u-cell-item title="学历"
								:border-top="false"
								:border-bottom="true"
								:label="xueli"
								:arrow="true"
								@click="selectXueli">
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
								:arrow="true"
								@click="selectBiyeTime">
							</u-cell-item>
							<u-cell-item title="现居住地"
								:border-top="false"
								:border-bottom="true"
								:label="juzhidizhi"
								:arrow="true"
								@click="selectCity">
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
				<view class="gongzuojinli"
					v-if="showList==1">
					<view class="gongzuojinli-cell">
						<view class="candidate-cell-name">
							<span class="userName">工作经历</span>
						</view>
						<view class="candidate-cell-icon"
							@click="onAddGongzuojingli">
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
				<view class="gongzuojinli-unknow"
					v-if="showList==0">
					<view class="gongzuojinli-cell">
						<u-cell-group :border="false">
							<u-cell-item title="工作经历"
								value="添加工作经历"
								:border-top="false"
								:border-bottom="false"
								:use-label-slot="false"
								:arrow="true"
								@click="onAddGongzuojingli">
							</u-cell-item>
						</u-cell-group>
						<view class="candidate-cell-name">
						</view>
					</view>
				</view>
			</view>
		</view>
		<u-select v-model="showCity"
			mode="mutil-column-auto"
			:list="cityList"
			@confirm="confirmCity"></u-select>
		<u-calendar v-model="showBiyeTime"
			@change="confirmBiyeTime"
			mode="date"></u-calendar>
		<u-select v-model="showSex"
			mode="mutil-column-auto"
			:list="sexList"
			@confirm="confirmSex"></u-select>
		<u-select v-model="showXueli"
			mode="mutil-column-auto"
			:list="xueliList"
			@confirm="confirmXueli"></u-select>
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
				showList: 0,
				text: "",
				zhantieText: "粘贴文本,自动识别候选人信息,支持同时识别多条信息。信息之间请尽量用标点隔开，并保证必填信息完整（身份证号可自动判断年龄、性别）",
				show: false,
				showCity: false,
				showBiyeTime: false,
				showSex: false,
				showXueli: false,
				username: "",
				phone: "",
				idCardNumber: "",
				sex: "请选择性别",
				year: "",
				xueli: "请选择学历",
				zhuangye: "",
				biyeTime: "请选择毕业时间（选填）",
				juzhidizhi: "请选择现居住地（选填）",
				xiangxidizhi: "",
				mianshiTime: "",
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
				}],
				cityList: [{
					value: 1,
					label: '中国',
					children: [{
						value: 2,
						label: '广东',
						children: [{
							value: 3,
							label: '深圳'
						}, {
							value: 4,
							label: '广州'
						}]
					}, {
						value: 5,
						label: '广西',
						children: [{
							value: 6,
							label: '南宁'
						}, {
							value: 7,
							label: '桂林'
						}]
					}]
				}, {
					value: 8,
					label: '美国',
					children: [{
						value: 9,
						label: '纽约',
						children: [{
							value: 10,
							label: '皇后街区'
						}]
					}]
				}],
				sexList: [{
					value: 0,
					label: '男性',
				}, {
					value: 1,
					label: '女性',
				}],
				xueliList: [{
					value: 2,
					label: '小学',
				}, {
					value: 3,
					label: '初中',
				}, {
					value: 4,
					label: '中专',
				}, {
					value: 5,
					label: '高中',
				}, {
					value: 6,
					label: '大专',
				}, {
					value: 7,
					label: '本科',
				}, {
					value: 8,
					label: '硕士研究生',
				}, {
					value: 9,
					label: '博士研究生',
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
			},
			// addgongzuojingli
			onAddGongzuojingli() {
				console.log("点击添加工作经历");
				uni.navigateTo({
					url: "/pages/candidateList/addgongzuojingli?id=1"
				})
			},
			selectCity() {
				console.log("点击选择城市");
				this.showCity = true;
			},
			confirmCity(e) {
				console.log("点击省市确定", e);
				console.log(e[0].label + "-" + e[1].label + "-" + e[2].label);
				this.juzhidizhi = e[1].label + "-" + e[2].label;
			},
			selectBiyeTime() {
				console.log("点击选择毕业时间");
				this.showBiyeTime = true;
			},
			confirmBiyeTime(e) {
				console.log("点击confirmEndTime", e);
				console.log("e.result:", e.result);
				this.biyeTime = e.result;
			},
			selectSex() {
				console.log("点击选择性别");
				this.showSex = true;
			},
			confirmSex(e) {
				console.log("点击confirmSex", e);
				console.log(e[0].label);
				this.sex = e[0].label;
			},
			selectXueli() {
				console.log("点击选择学历");
				this.showXueli = true;
			},
			confirmXueli(e) {
				console.log("点击confirmXueli", e);
				console.log(e[0].label);
				this.xueli = e[0].label;
			},
			shibie() {
				console.log("点击识别按钮");
				uni.showModal({
					title: '提交成功',
					content: '等待后端返回数据',
					showCancel: false,
					success: function(res) {
						if (res.confirm) {
							console.log('用户点击确定');
						}
					}
				});
			},
			// addgongzuojingli
			onAddGongzuojingli() {
				console.log("点击添加工作经历");
				uni.navigateTo({
					url: "/pages/candidateList/addgongzuojingli?id=1"
				})
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

			.zhantie {
				background-color: #ffffff;
				padding: 30rpx;
				margin-bottom: 30rpx;
				margin-left: 20rpx;
				margin-right: 20rpx;
				border-radius: 18rpx;

				.zhantie-input {
					width: 100%;
					margin-top: 10rpx;
					margin-bottom: 10rpx;
					padding-left: 25rpx;
					padding-right: 25rpx;
				}

				.zhantie-button {
					text-align: right;
					margin-top: 20rpx;
					margin-right: 30rpx;
				}
			}

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

				.gongzuojinli-unknow {
					height: 180rpx;
					background-color: #ffffff;
					padding: 30rpx;
					margin-bottom: 180rpx;
					margin-left: 20rpx;
					margin-right: 20rpx;
					border-radius: 18rpx;

					.gongzuojinli-cell {
						width: 100%;
						height: 60rpx;
						margin-top: 10rpx;
						margin-bottom: 10rpx;
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
