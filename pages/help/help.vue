<template>
	<view class="container">
		<view class="tabs">
			<u-tabs :list="tabsList"
				active-color="#ffaa00"
				:current="tabsCurrent"
				:is-scroll="false"
				@change="changeTabs"></u-tabs>
		</view>
		<view class="help-body">
			<view v-if="tabsCurrent==0"
				class="help-list">
				<u-cell-group>
					<view v-for="(item,index) in helpList1"
						:key="index">
						<u-cell-item :title="item.text"
							@click="todetail(item.id)"></u-cell-item>
					</view>
				</u-cell-group>
			</view>
			<view v-if="tabsCurrent==1"
				class="help-list">
				<u-cell-group>
					<view v-for="(item,index) in helpList2"
						:key="index">
						<u-cell-item :title="item.text"
							@click="todetail(item.id)"></u-cell-item>
					</view>
				</u-cell-group>
			</view>
			<view v-if="tabsCurrent==2"
				class="help-list">
				<u-cell-group>
					<view v-for="(item,index) in helpList3"
						:key="index">
						<u-cell-item :title="item.text"
							@click="todetail(item.id)"></u-cell-item>
					</view>
				</u-cell-group>
			</view>
			<view v-if="tabsCurrent==3"
				class="help-list">
				<u-cell-group>
					<view v-for="(item,index) in helpList4"
						:key="index">
						<u-cell-item :title="item.text"
							@click="todetail(item.id)"></u-cell-item>
					</view>
				</u-cell-group>
			</view>
			<view class="help-bottom">
				<u-divider color="#868686"
					height="20rpx"
					half-width="200"
					bg-color="#f5f5f5"
					border-color="#6d6d6d">已经到底了</u-divider>
			</view>
		</view>
		<view v-if="listlength == 0"
			class="kong">
			<u-empty text="暂无更多"
				:src="noOrderDataImageURL"></u-empty>
		</view>
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	export default {
		data() {
			return {
				listlength: 1,
				tabsList: [{
					name: '账号管理'
				}, {
					name: '资质认证'
				}, {
					name: '订单管理'
				}, {
					name: '结算相关'
				}],
				tabsCurrent: 0,
				noOrderDataImageURL: 'https://me.heimaoba.cn/static/image/noOrderData.png',
				helpList1: homeData.helpList.helpList1,
				helpList2: homeData.helpList.helpList2,
				helpList3: homeData.helpList.helpList3,
				helpList4: homeData.helpList.helpList4,
			}
		},
		methods: {
			changeTabs(index) {
				console.log("changeTabs:", index);
				this.tabsCurrent = index;
			},
			todetail(id) {
				console.log("todetail-id:", id);
				uni.navigateTo({
					url: "/pages/help/helpdetail"
				})
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
			margin-bottom: 5rpx;
		}

		.help-body {
			background-color: #fff;

			.help-list {
				background-color: #fff;
			}

			.help-bottom {
				background-color: #fff;
			}
		}

		.kong {
			width: 100%;
			margin-top: 300rpx;
		}
	}
</style>
