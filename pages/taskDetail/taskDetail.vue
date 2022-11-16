<template>
	<view class="container">
		<view class="zhiWeiList">
			<view class="zhiWei-head">
				<view class="zhiWei-tittle">{{ item.name }}</view>
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
		</view>
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	export default {
		data() {
			return {
				item: homeData.teskDetaildata
			}
		},
		onLoad: function(option) {
			console.log("option:", option);
			console.log("option.id:", option.id);
			console.log("this.item:", this.item);
		},
		methods: {}
	}
</script>
<style>
	page {
		background-color: #cccccc47;
	}
</style>
<style lang="scss"
	scoped>
	.container {
		width: 100%;
		height: 200vh;

		.zhiWeiList {
			margin-bottom: 20rpx;
			margin-left: 20rpx;
			margin-right: 20rpx;
			margin-top: 30rpx;
			height: 300rpx;
			background-color: #fff;
			border-radius: 15px;

			.zhiWei-head {
				padding: 10rpx;

				.zhiWei-tittle {
					height: 50rpx;
					font-size: 18px;
					font-weight: 1000;
					float: left;
					margin-top: 10rpx;
					padding-left: 20rpx;
				}
			}

			.zhiWei-biaoqian {
				margin-top: 50rpx;

				.zhiWei-fuli {
					float: left;
					padding-left: 20rpx;
					padding-bottom: 20rpx;
					display: flex;
					width: 100%;

					.zhiWei-fuli-list {
						align-items: center;
						margin-right: 10rpx;
					}
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
		}
	}
</style>
