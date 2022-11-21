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
			<z-task-list :dataList="zZhiweiData"
				@send_addHouXuanRen="addHouXuanRen"></z-task-list>
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
		<u-popup v-model="showAddHouXuanRen"
			mode="bottom"
			border-radius="14"
			:safe-area-inset-bottom="true"
			length="45%">
			<view class="houxuanren">
				<view class="houxuanren-tittle"> 添加候选人 </view>
				<view class="houxuanren-cell">
					<u-cell-group :border="false">
						<u-cell-item title="添加候选人"
							label="支持自动解析剪贴板信息,批量添加多个"
							:border-top="false"
							:border-bottom="false"
							:arrow="true"
							@click="callPhone">
							<view class="lefticon"
								slot="icon">
								<u-icon size="60"
									name="account"></u-icon>
							</view>
						</u-cell-item>
						<u-cell-item title="邀请候选人扫码"
							label="发送职位二维码,邀请候选人主动报名"
							:border-top="false"
							:border-bottom="false"
							:arrow="true">
							<view class="lefticon"
								slot="icon">
								<u-icon size="60"
									name="email"></u-icon>
							</view>
						</u-cell-item>
						<u-cell-item title="Excel批量导入"
							label="通过Excel模板批量添加"
							:border-top="false"
							:border-bottom="false"
							:arrow="true">
							<view class="lefticon"
								slot="icon">
								<u-icon size="60"
									name="list-dot"></u-icon>
							</view>
						</u-cell-item>
					</u-cell-group>
				</view>
			</view>
		</u-popup>
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
				showAddHouXuanRen: false,
				itemCache: [],
			}
		},
		methods: {
			changeTabs(index) {
				console.log("changeTabs:", index);
				this.tabsCurrent = index;
			},
			addHouXuanRen(item) {
				console.log("父组件的addHouXuanRen", item);
				this.itemCache = item;
				this.showAddHouXuanRen = true;
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

		.houxuanren {
			padding-top: 20rpx;

			.houxuanren-tittle {
				margin: 20rpx;
				height: 30rpx;
				line-height: 30rpx;
				font-size: 38rpx;
				font-weight: 1000;
			}

			.houxuanren-cell {
				padding-top: 20rpx;

				.lefticon {
					margin-right: 30rpx;
				}
			}
		}
	}
</style>
