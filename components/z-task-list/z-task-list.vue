<template>
	<view class="container">
		<view class="taskList"
			v-for="(item, index)  in dataList"
			:key="index">
			<view class="task-head">
				<view class="task-tittle">{{ item.name }}
					<u-icon class="sIcon"
						@click="canceSearch"
						name="arrow-right"
						color="#000000"
						size="30"></u-icon>
				</view>
				<view class="task-jindu">
					<view class="task-jinxing">进行中</view>
					<!-- <view class="task-jieshu">已结束</view> -->
				</view>
			</view>
			<view class="task-xingzhi"> {{ item.area }}|{{ item.peopleNumber }}|薪酬{{ item.taskMoney }}
				{{ item.taskMoneyType }}
			</view>
			<view class="task-info">
				<view class="wrap">
					<u-row gutter="16">
						<u-col span="4">
							<view class="col-layout-info">1</view>
						</u-col>
						<u-col span="4">
							<view class="col-layout-info">0</view>
						</u-col>
						<u-col span="4">
							<view class="col-layout-info">0</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="4">
							<view class="col-layout-tittle">全部候选人</view>
						</u-col>
						<u-col span="4">
							<view class="col-layout-tittle">已入职</view>
						</u-col>
						<u-col span="4">
							<view class="col-layout-tittle">已过保</view>
						</u-col>
					</u-row>
				</view>
			</view>
			<view class="task-line">
				<u-line color="#9e9e9e" />
			</view>
			<view class="task-footer">
				<view class="task-caozuo">
					<u-button size="mini"
						:plain="true"
						type="warning">添加候选人</u-button>
				</view>
				<view class="task-caozuo">
					<u-button size="mini"
						:plain="true"
						@click="tokefu(item)"
						type="info">联系顾问</u-button>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		name: "z-task-list",
		props: {
			dataList: {
				type: Array,
				default: []
			}
		},
		data() {
			return {};
		},
		mounted() {
			console.log(this.dataList);
		},
		methods: {
			tokefu(item) {
				console.log("点击事件触发toDetail--item：", item);
				uni.redirectTo({
					url: "/pages/taskDetail/lianxikefu?id=" + item.id
				})
			}
		}
	}
</script>
<style lang="scss"
	scoped>
	.taskList {
		margin: 20rpx;
		height: 380rpx;
		background-color: #fff;
		border-radius: 15px;

		.task-head {
			padding: 10rpx;

			.task-tittle {
				font-size: 18px;
				font-weight: 1000;
				float: left;
				margin-top: 10rpx;
				padding-left: 20rpx;
			}

			.task-jindu {
				float: right;
				padding-right: 20rpx;
				margin-top: 10rpx;
				display: flex;

				.task-jinxing {
					align-items: center;
					color: #00b500;
				}

				.task-jieshu {
					align-items: center;
					color: #ff0000
				}
			}
		}

		.task-xingzhi {
			width: 100%;
			float: left;
			margin-top: 10rpx;
			padding-left: 20rpx;
		}

		.task-info {
			width: 100%;
			height: 220rpx;
			float: inherit;
		}

		.task-line {
			/* #ifdef H5 */
			margin-top: 20px;
			/* #endif */
			/* #ifndef H5 */
			margin-top: 10rpx;
			/* #endif */
			padding: 10rpx;
			float: inherit;
		}

		.task-footer {
			padding: 20rpx;

			.task-caozuo {
				float: right;
				margin-right: 20rpx;
			}
		}
	}

	.wrap {
		padding-top: 116rpx;
		padding-right: 66rpx;
		padding-bottom: 86rpx;
		padding-left: 66rpx;
	}

	.u-row {
		margin-top: 24rpx;
		margin-left: 10rpx;
		margin-right: 10rpx;
	}

	.col-layout-info {
		/* #ifdef H5 */
		height: 17px;
		/* #endif */
		/* #ifndef H5 */
		height: 36rpx;
		/* #endif */
		border-radius: 8rpx;
		color: #000000;
		text-align: center;
		font-size: 40rpx;
		font-weight: 1000;
	}

	.col-layout-tittle {
		/* #ifdef H5 */
		height: 18px;
		margin-top: 4px;
		/* #endif */
		/* #ifndef H5 */
		height: 60rpx;
		margin-top: 20rpx;
		/* #endif */
		border-radius: 8rpx;
		color: #545454;
		text-align: center;
	}
</style>
