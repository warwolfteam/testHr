<template>
	<view class="container">
		<view class="bg">
			<view class="myinfo">
				<view class="myinfo-tittle"> 基本信息 </view>
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item title="江西七善科技有限公司"
							label="91360781MA37Q8Q32U"
							:border-top="false"
							:border-bottom="true"
							:arrow="true"
							@click="toEditInfo"></u-cell-item>
						<u-cell-item title="联系地址"
							label="未填写"
							:border-top="false"
							:border-bottom="true"
							:arrow="false"></u-cell-item>
						<u-cell-item title="联系人姓名/电话"
							label="周**/181*****718"
							:border-top="false"
							:border-bottom="false"
							:arrow="false"></u-cell-item>
					</u-cell-group>
				</view>
			</view>
			<view class="myinfo">
				<view class="myinfo-tittle"> 业务擅长 </view>
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item title="业务覆盖城市"
							label="赣州"
							:border-top="false"
							:border-bottom="true"
							:arrow="false"></u-cell-item>
						<u-cell-item title="擅长岗位分类"
							label="销售"
							:border-top="false"
							:border-bottom="true"
							:arrow="false"></u-cell-item>
						<u-cell-item title="可输出人数规模"
							label="51-100人"
							:border-top="false"
							:border-bottom="false"
							:arrow="false"></u-cell-item>
					</u-cell-group>
				</view>
			</view>
			<view class="myinfo">
				<view class="myinfo-tittle"> 收款账户 </view>
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item title="台州银行"
							label="6400 01** ***0 015"
							:border-top="false"
							:border-bottom="false"
							:arrow="true"
							@click="toEditBank"></u-cell-item>
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
			return {}
		},
		methods: {
			toEditBank() {
				console.log("点击收款账户");
				uni.navigateTo({
					url: "/pages/myinfo/bank"
				})
			},
			toEditInfo() {
				console.log("点击基本信息");
				uni.navigateTo({
					url: "/pages/myinfo/info"
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

		// height: 200vh;
		.bg {
			background-color: #e7e7e7;
			padding-top: 30rpx;
			padding-bottom: 30rpx;

			.myinfo {
				background-color: #ffffff;
				padding: 60rpx;
				margin-bottom: 20rpx;
				margin-left: 20rpx;
				margin-right: 20rpx;
				border-radius: 18rpx;

				.myinfo-tittle {
					margin-left: 30rpx;
					font-size: 38rpx;
					font-weight: 1000;
				}

				.myinfo-cell {
					margin-top: 20rpx;
				}
			}
		}
	}
</style>
