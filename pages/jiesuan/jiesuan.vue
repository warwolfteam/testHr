<template>
	<view class="container">
		<view class="tabs">
			<u-tabs :list="tabsList"
				active-color="#ffaa00"
				:current="tabsCurrent"
				@change="changeTabs"></u-tabs>
		</view>
		<view class="order-bottom">
			<u-divider color="#868686"
				height="20rpx"
				half-width="200"
				bg-color="#cccccc47"
				border-color="#6d6d6d">已经到底了</u-divider>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				tabsList: [{
					name: '进行中'
				}, {
					name: '已结束'
				}],
				tabsCurrent: 0,
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
		background-color: #cccccc47;

		.tabs {
			margin-bottom: 20px;
		}

		.order-bottom {
			background-color: #fff;
		}
	}
</style>
