<template>
	<view class="container">
		<view class="tabs">
			<u-tabs :list="tabsList"
				active-color="#ffaa00"
				:current="tabsCurrent"
				:is-scroll="false"
				@change="changeTabs"></u-tabs>
		</view>
		<view class="kong">
			<u-empty text="暂无更多"
				:src="noOrderDataImageURL"></u-empty>
		</view>
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
		height: 100vh;

		.tabs {
			margin-bottom: 20px;
		}

		.kong {
			width: 100%;
			margin-top: 300rpx;
		}
	}
</style>
