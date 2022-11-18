<template>
	<view class="container">
		<view class="tabs">
			<u-tabs :list="tabsList"
				active-color="#ffaa00"
				:current="tabsCurrent"
				:is-scroll="false"
				@change="changeTabs"></u-tabs>
		</view>
		<view class="zanwu">
			<u-image :src="noOrderDataImageURL"
				width="50%"
				height="50%"></u-image>
			<span class="zanwu-zi">暂无更多</span>
		</view>
		<!-- 		<view class="order-bottom">
			<u-divider color="#868686"
				height="20rpx"
				half-width="200"
				bg-color="#cccccc47"
				border-color="#6d6d6d">已经到底了</u-divider>
		</view> -->
	</view>
</template>
<script>
	export default {
		data() {
			return {
				tabsList: [{
					name: '全部'
				}, {
					name: '待确认'
				}, {
					name: '结算中'
				}, {
					name: '已结算'
				}, {
					name: '其他'
				}],
				tabsCurrent: 0,
				noOrderDataImageURL: 'https://me.heimaoba.cn/static/image/noOrderData.png',
			}
		},
		methods: {
			changeTabs(index) {
				console.log("changeTabs:", index);
				this.tabsCurrent = index;
			}
		}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #f5f5f5;
		width: 100%;
		height: 100%;

		.tabs {
			margin-bottom: 20px;
		}

		.zanwu {
			width: 100%;
			height: 700rpx;
			margin: 180rpx;
			background-color: #f5f5f5;
			text-align: left;

			.zanwu-zi {
				width: 60%;
				color: #787878;
				margin-left: 130rpx;
				padding-top: 300rpx;
			}
		}

		.order-bottom {
			background-color: #f5f5f5;
		}
	}
</style>
