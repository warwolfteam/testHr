<template>
	<view class="container">
		<view class="select">
			<u-dropdown>
				<u-dropdown-item v-model="selectValue"
					@change="changeSelect"
					:title="selectTitle"
					:options="selectOptions"></u-dropdown-item>
			</u-dropdown>
		</view>
		<view class="bg">
			<!-- 候选人列表 -->
			<view class="allList"
				v-for="(item, index)  in dataList"
				:key="index"
				v-if="selectValue == 0&1">
				<view class="candidate"
					@click="toCandidateDetail(item)">
					<view class="candidate-cell">
						<view class="candidate-cell-name">
							<span class="userName">{{item.label}}</span>
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
				</view>
			</view>
			<!-- 已经到底了 -->
			<view class="order-bottom"
				v-if="selectValue == 0&1">
				<u-divider color="#868686"
					height="20rpx"
					half-width="200"
					bg-color="#dedede47"
					border-color="#6d6d6d">已经到底了</u-divider>
			</view>
			<view class="kong"
				v-if="selectValue != 0&1">
				<u-empty text="暂无候选人"
					:src="noOrderDataImageURL"></u-empty>
			</view>
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
				noOrderDataImageURL: 'https://me.heimaoba.cn/static/image/noOrderData.png',
				selectValue: 0,
				selectTitle: "新添加（1）",
				selectOptions: [{
					label: '全部招聘状态（1）',
					value: 0,
				}, {
					label: '新添加（1）',
					value: 1,
				}, {
					label: '已到面',
					value: 2,
				}, {
					label: '已入职',
					value: 3,
				}, {
					label: '已过保',
					value: 4,
				}, {
					label: '不合适',
					value: 5,
				}],
				dataList: [{
					label: '张三',
					id: 0,
				}, {
					label: '李四',
					id: 1,
				}, {
					label: '王五',
					id: 2,
				}, {
					label: '赵六',
					id: 3,
				}, {
					label: '周七',
					id: 4,
				}, {
					label: '钱八',
					id: 5,
				}],
			}
		},
		onLoad: function(option) {
			console.log("option:", option);
			console.log("option.selectStatus:", option.selectStatus);
			this.selectValue = option.selectStatus
			this.selectTitle = this.selectOptions[option.selectStatus].label
		},
		methods: {
			toEditInfo() {
				console.log("点击解除与认证主体绑定");
			},
			changeSelect(e) {
				console.log("点击下拉", e);
				console.log("点击下拉", this.selectOptions);
				console.log("点击下拉", this.selectValue);
				this.selectTitle = this.selectOptions[e].label
			},
			toCandidateDetail(item) {
				console.log("点击候选人", item);
				uni.navigateTo({
					url: "/pages/candidateDetail/candidateDetail?id=" + item.id
				})
			},
		}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #a2a2a247;
		width: 100%;
		height: 100vh;

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
					height: 180rpx;
					background-color: #ffffff;
					padding: 30rpx;
					margin-bottom: 20rpx;
					margin-left: 10rpx;
					margin-right: 10rpx;
					border-radius: 18rpx;

					.candidate-tittle {
						margin-left: 30rpx;
						font-size: 38rpx;
						font-weight: 1000;
					}

					.candidate-cell {
						width: 100%;
						height: 50rpx;
						margin-top: 10rpx;
						margin-bottom: 10rpx;

						.candidate-cell-name {
							float: left;
							display: flex;

							.userName {
								align-items: center;
								margin-right: 20rpx;
							}

							.sexIcon {
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
	}
</style>
