<template>
	<view class="container">
		<view class="zhiWeiList"
			v-for="(item, index)  in dataList"
			:key="index">
			<view class="zhiWei-head">
				<view class="zhiWei-tittle">{{ item.name }}</view>
				<view class="zhiWei-money">
					<view class="zhiWei-yuan">{{ item.money }}</view>
					<view class="zhiWei-miaosu">{{ item.moneyType }}</view>
				</view>
			</view>
			<view class="zhiWei-biaoqian">
				<view class="zhiWei-fuli">
					<view class="zhiWei-fuli-list"
						v-if="item.fulilist.length >= 1"
						v-for="tags in item.fulilist"
						:key="tags.id">
						<u-tag :text="tags.text"
							:type="tags.type"
							:mode="tags.mode" />
					</view>
				</view>
				<view class="zhiWei-fanxian"
					v-if="item.fanxian">
					<u-tag :text="item.fanxian"
						type="warning"
						mode="light" />
				</view>
			</view>
			<view class="zhiWei-xingzhi"> {{ item.area }}|{{ item.peopleNumber }}|薪酬{{ item.taskMoney }}
				{{ item.taskMoneyType }}
			</view>
			<view class="zhiWei-jindu-all">
				<view class="zhiWei-jindu">
					<view class="zhiWei-jindu-tittle"> 招聘进度：{{ item.zhaopingjindu }}% </view>
					<view class="zhiWei-jindu-line">
						<u-line-progress :striped="true"
							:percent="item.zhaopingjindu"
							:striped-active="true"></u-line-progress>
					</view>
				</view>
			</view>
			<view class="zhiWei-line">
				<u-line color="#9e9e9e" />
			</view>
			<view class="zhiWei-footer">
				<view class="zhiWei-qiyexinxi">
					<view class="zhiWei-qiyexinxi-icon">
						<u-icon size="30"
							name="home"></u-icon>
					</view>
					<view class="zhiWei-qiyexinxi-text">{{ item.enterpriseName }} </view>
				</view>
				<view class="zhiWei-time"> {{ item.releaseTime }} </view>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		name: "z-zhiwei-list",
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
		}
	}
</script>
<style lang="scss"
	scoped>
	.zhiWeiList {
		margin: 20rpx;
		height: 350rpx;
		background: #fff;

		.zhiWei-head {
			// margin-top: 50rpx;
			padding: 10rpx;

			.zhiWei-tittle {
				float: left;
				margin-top: 10rpx;
				padding-left: 20rpx;
			}

			.zhiWei-money {
				float: right;
				padding-right: 20rpx;
				margin-top: 10rpx;
				display: flex;

				.zhiWei-yuan {
					align-items: center;
					color: #ff9800;
				}

				.zhiWei-miaosu {
					align-items: center;
					color: #ccc
				}
			}
		}

		.zhiWei-biaoqian {
			margin-top: 50rpx;

			.zhiWei-fuli {
				float: left;
				padding-left: 20rpx;
				padding-bottom: 20rpx;
				display: flex;

				.zhiWei-fuli-list {
					align-items: center;
				}
			}

			.zhiWei-fanxian {
				float: right;
				padding-right: 20rpx;
			}
		}

		.zhiWei-xingzhi {
			width: 100%;
			float: left;
			margin-top: 10rpx;
			padding-left: 20rpx;
		}

		.zhiWei-jindu-all {
			margin-top: 30rpx;
			float: left;
			width: 100%;
			padding-left: 20rpx;

			.zhiWei-jindu {
				display: flex;

				.zhiWei-jindu-tittle {
					align-items: center;
					margin-right: 5%;
				}

				.zhiWei-jindu-line {
					width: 60%;
					align-items: center;
				}
			}
		}

		.zhiWei-line {
			margin-top: 220rpx;
			padding: 20rpx;
			float: inherit;
		}

		.zhiWei-footer {
			// margin-top: 10rpx;
			padding: 20rpx;

			.zhiWei-qiyexinxi {
				float: left;
				// margin-top: 10rpx;
				display: flex;

				.zhiWei-qiyexinxi-icon {
					align-items: center;
				}

				.zhiWei-qiyexinxi-text {
					align-items: center;
				}
			}

			.zhiWei-time {
				float: right;
				// margin-top: 10rpx;
			}
		}
	}
</style>
