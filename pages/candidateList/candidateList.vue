<template>
	<view class="container">
		<view class="select">
			<u-dropdown>
				<u-dropdown-item v-model="selectValue"
					@change="changeSelect"
					:title="selectTitle"
					:options="selectOptions"></u-dropdown-item>
			</u-dropdown>
		</view>
		<view class="bg">
			<view class="candidate">
				<view class="candidate-cell">
					<view class="candidate-cell-name">
						<span class="userName">张三</span>
						<span class="sexIcon">
							<i class="iconfont icon-nvxing"></i>
						</span>
					</view>
					<view class="candidate-cell-status"> 新添加 </view>
				</view>
				<view class="candidate-miaosu">
					<view class="candidate-miaosu-xinxi">
						<span class="xinxi">男 | 31岁 | 大专</span>
					</view>
					<view class="candidate-miaosu-time"> 2天前 </view>
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
				show: false,
				selectValue: "0",
				selectTitle: "新添加（1）",
				selectOptions: [{
					label: '全部招聘状态（1）',
					value: 0,
				}, {
					label: '新添加（1）',
					value: 1,
				}, {
					label: '已到面',
					value: 2,
				}, {
					label: '已入职',
					value: 3,
				}, {
					label: '已过保',
					value: 4,
				}, {
					label: '不合适',
					value: 5,
				}],
			}
		},
		methods: {
			toEditInfo() {
				console.log("点击解除与认证主体绑定");
			},
			changeSelect(e) {
				console.log("点击下拉", e);
				console.log("点击下拉", this.selectOptions);
				this.selectTitle = this.selectOptions[e].label
			}
		}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #a2a2a247;
		width: 100%;
		height: 100vh;

		.select {
			background-color: #ffffff;
			margin-bottom: 20rpx;
		}

		.bg {
			// background-color: #e7e7e7;
			padding-top: 30rpx;
			padding-bottom: 30rpx;

			.candidate {
				height: 180rpx;
				background-color: #ffffff;
				padding: 30rpx;
				margin-bottom: 20rpx;
				margin-left: 10rpx;
				margin-right: 10rpx;
				border-radius: 18rpx;

				.candidate-tittle {
					margin-left: 30rpx;
					font-size: 38rpx;
					font-weight: 1000;
				}

				.candidate-cell {
					width: 100%;
					height: 50rpx;
					margin-top: 10rpx;
					margin-bottom: 10rpx;

					.candidate-cell-name {
						float: left;
						display: flex;

						.userName {
							align-items: center;
							margin-right: 20rpx;
						}

						.sexIcon {
							align-items: center;
							font-size: 18rpx;
							color: #0055ff;
						}
					}

					.candidate-cell-status {
						float: right;
					}
				}

				.candidate-miaosu {
					width: 100%;
					height: 50rpx;
					margin-top: 10rpx;
					margin-bottom: 10rpx;

					.candidate-miaosu-xinxi {
						float: left;
						display: flex;

						.xinxi {
							align-items: center;
							font-size: 24rpx;
							color: #717171;
						}
					}

					.candidate-miaosu-time {
						float: right;
						font-size: 24rpx;
						color: #717171;
					}
				}
			}
		}
	}
</style>
