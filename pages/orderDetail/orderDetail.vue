<template>
	<view class="container">
		<view class="bg">
			<view class="myinfo">
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item :title="zhiwuName"
							@click="toTaskDetail"
							value="任务详情"
							:border-top="false"
							:border-bottom="false"
							:arrow="true"></u-cell-item>
					</u-cell-group>
				</view>
			</view>
			<view class="myinfo">
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item title="接单人数"
							hover-class="none"
							:value="jiedanNumber"
							:border-top="false"
							:border-bottom="true"
							:arrow="false"></u-cell-item>
						<u-cell-item title="结算方式"
							hover-class="none"
							:value="jiesuanType"
							:border-top="false"
							:border-bottom="true"
							:arrow="false"></u-cell-item>
						<u-cell-item title="结算条件"
							hover-class="none"
							:value="jiesuanIf"
							:border-top="false"
							:border-bottom="true"
							:arrow="false"></u-cell-item>
						<u-cell-item title="结算价格"
							hover-class="none"
							:border-top="false"
							:border-bottom="true"
							:arrow="false">
							<view slot="right-icon"
								class="jiage">
								<span class="jiage-jiesuanMoney">{{jiesuanMoney}}</span>/人
							</view>
						</u-cell-item>
						<u-cell-item title="接单时间"
							hover-class="none"
							:value="jiedanTime"
							:border-top="false"
							:border-bottom="false"
							:arrow="false"></u-cell-item>
					</u-cell-group>
				</view>
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
				zhiwuName: "电销客服",
				jiedanNumber: "20人",
				jiesuanType: "一次性返",
				jiesuanIf: "到岗+质保3天",
				jiesuanMoney: "***",
				jiedanTime: "2022-11-14 21:55",
				id: "1"
			}
		},
		methods: {
			toTaskDetail() {
				console.log("去任务详情");
				uni.navigateTo({
					url: "/pages/taskDetail/taskDetail?id=" + this.id
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

					.jiage {
						color: #000;

						.jiage-jiesuanMoney {
							font-size: 38rpx;
							color: #ff641c;
							font-weight: 1000;
						}
					}
				}
			}
		}
	}
</style>
