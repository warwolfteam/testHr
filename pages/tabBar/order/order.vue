<template>
	<view class="container">
		<view class="home-search-area">
			<u-search placeholder="搜索任务名称"
				margin="40rpx"
				:show-action="false"
				v-model="keyword">
			</u-search>
		</view>
		<view class="tabs">
			<u-tabs :list="tabsList"
				active-color="#ffaa00"
				:current="tabsCurrent"
				@change="changeTabs"></u-tabs>
		</view>
		<view class="order-body"
			v-if="tabsCurrent==0">
			<z-task-list :dataList="zZhiweiData"></z-task-list>
			<view class="order-bottom">
				<u-divider color="#868686"
					height="20rpx"
					half-width="200"
					bg-color="#cccccc47"
					border-color="#6d6d6d">已经到底了</u-divider>
			</view>
		</view>
		<view class="kong"
			v-if="tabsCurrent==1">
			<u-empty text="暂无已结束的订单"
				:src="noOrderDataImageURL"></u-empty>
		</view>
	</view>
</template>
<script>
	import zTaskList from '@/components/z-task-list/z-task-list.vue'
	import homeData from '@/common/home-data.js'
	export default {
		components: {
			zTaskList
		},
		data() {
			return {
				keyword: "",
				tabsList: [{
					name: '进行中'
				}, {
					name: '已结束'
				}],
				tabsCurrent: 0,
				zZhiweiData: homeData.zZhiweiData.data.list,
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
		background-color: #cccccc47;

		// height: 100%;
		// margin-top: 150rpx;
		.home-search-area {
			padding: 5rpx;
			display: flex;
			background-color: #fff;
		}

		.tabs {
			padding-bottom: 20px;
			background-color: #fff;
		}

		.order-body {
			width: 100%;

			.order-bottom {
				background-color: #fff;
			}
		}

		.kong {
			width: 100%;
			height: 50vh;
			background-color: #fff;
		}
	}
</style>
