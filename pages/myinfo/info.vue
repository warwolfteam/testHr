<template>
	<view class="container">
		<view class="bg">
			<view class="myinfo">
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item title="解除与认证主体绑定"
							label="如您已不负责此团队的招聘业务,可解除绑定"
							:border-top="false"
							:border-bottom="false"
							:arrow="true"
							@click="toEditInfo"></u-cell-item>
					</u-cell-group>
				</view>
			</view>
		</view>
		<u-modal v-model="show"
			:show-cancel-button="true"
			:content="content"></u-modal>
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	export default {
		components: {},
		data() {
			return {
				show: false,
				content: '确认解除当前账户与认证主体绑定？'
			}
		},
		methods: {
			toEditInfo() {
				console.log("点击解除与认证主体绑定");
				this.show = true;
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

		.bg {
			background-color: #e7e7e7;
			padding-top: 30rpx;
			padding-bottom: 30rpx;

			.myinfo {
				background-color: #ffffff;
				padding: 60rpx;
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
				}
			}
		}
	}
</style>
