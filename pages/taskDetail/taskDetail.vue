<template>
	<view class="container">
		<!-- 任务基本信息 -->
		<view class="zhiWei">
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
		<!-- 任务返佣信息 -->
		<view class="fanyong">
			<view class="fanyong-head">
				<view class="fanyong-tittle">佣金</view>
				<view class="fanyong-tip">
					<u-icon @click="onFanYongTip()"
						name="question-circle"
						color="#9e9e9e"
						size="40"></u-icon>
				</view>
			</view>
			<view class="fanyong-img"
				:style="{backgroundImage:                             
				        'url('+imageURL+')'}">
				<view class="fanyong-money"> 一次性返 <span class="onmoney"> {{ item.fanyongxinxi.fanYongMoney }}元</span>/人
				</view>
				<view class="fanyong-tips"> {{ item.fanyongxinxi.tips }} </view>
			</view>
			<view class="fanyong-jiesuan">
				<span>结算条件： {{ item.fanyongxinxi.jiwsuantiaojian }}</span>
			</view>
		</view>
		<!-- 任务岗位详情 -->
		<view class="ganwei">
			<view class="ganwei-tittle">岗位详情</view>
			<view class="ganwei-zhiwei">客服</view>
			<view class="ganwei-info-fuli">
				<span class="ganwei-info-tittle">薪资福利</span>
				<view class="wrap">
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">薪酬 </view>
						</u-col>
						<u-col span="6">
							<view class="col-layout-tittle">薪酬结构</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-info">5000-10000元/月</view>
						</u-col>
						<u-col span="6">
							<view class="col-layout-info">底薪,绩效,提成,加班费</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">发薪周期</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-info">月</view>
						</u-col>
					</u-row>
				</view>
			</view>
			<view class="ganwei-info-didian">
				<span class="ganwei-info-tittle">工作时间地点</span>
				<view class="wrap">
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">工作时间</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-info">早九晚六</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">出勤制度</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="10">
							<view class="col-layout-info">周末双休</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">工作地点</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="10">
							<view class="col-layout-info">全国</view>
						</u-col>
					</u-row>
				</view>
			</view>
			<view class="ganwei-info-yaoqiu">
				<span class="ganwei-info-tittle">岗位要求</span>
				<view class="wrap">
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">年龄</view>
						</u-col>
						<u-col span="6">
							<view class="col-layout-tittle">性别</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-info">不限</view>
						</u-col>
						<u-col span="6">
							<view class="col-layout-info">不限</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">学历</view>
						</u-col>
						<u-col span="6">
							<view class="col-layout-tittle">工作经验</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-info">不限</view>
						</u-col>
						<u-col span="6">
							<view class="col-layout-info">不限</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">专业要求</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="10">
							<view class="col-layout-info">不限</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">技能要求</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="10">
							<view class="col-layout-info">不限</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="6">
							<view class="col-layout-tittle">岗位职责</view>
						</u-col>
					</u-row>
					<u-row gutter="16">
						<u-col span="10">
							<view class="col-layout-info">负责早教产的电话销售工作</view>
						</u-col>
					</u-row>
				</view>
			</view>
			<view class="ganwei-info-qiye">
				<span class="ganwei-info-tittle">用工企业</span>
				<view class="wrap">
					<u-row gutter="16">
						<u-col span="1">
							<view class="col-layout-info">
								<u-icon size="30"
									name="home"></u-icon>
							</view>
						</u-col>
						<u-col span="8">
							<view class="col-layout-info">倍乐生商贸（中国）有限公司</view>
						</u-col>
					</u-row>
				</view>
			</view>
		</view>
		<!-- 以下为弹出层 -->
		<u-toast ref="fanYongToast" />
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	export default {
		data() {
			return {
				item: homeData.teskDetaildata,
				imageURL: 'https://me.heimaoba.cn/static/image/fanyongdetail.png'
			}
		},
		onLoad: function(option) {
			console.log("option:", option);
			console.log("option.id:", option.id);
			console.log("this.item:", this.item);
		},
		methods: {
			onFanYongTip() {
				console.log("点击返佣提示按钮");
				this.showFanYongToast();
			},
			showFanYongToast() {
				console.log("触发提示");
				this.$refs.fanYongToast.show({
					title: '候选人过保后一次性返费',
					type: "info"
				})
			}
		}
	}
</script>
<style>
	page {
		background-color: #cccccc47;
	}
</style>
<style lang="scss"
	scoped>
	.wrap {
		padding: 24rpx;
	}

	.u-row {
		margin-top: 40rpx;
		margin-bottom: 40rpx;
		margin-left: 10rpx;
		margin-right: 10rpx;
	}

	.col-layout-tittle {
		/* #ifdef H5 */
		height: 17px;
		/* #endif */
		/* #ifndef H5 */
		height: 36rpx;
		/* #endif */
		border-radius: 8rpx;
		color: #9aa1a8;
	}

	.col-layout-info {
		/* #ifdef H5 */
		height: 22px;
		/* #endif */
		/* #ifndef H5 */
		height: 60rpx;
		/* #endif */
		border-radius: 8rpx;
		color: #000000;
	}

	.bg-purple {
		background: #d3dce6;
	}

	.bg-purple-light {
		background: #e5e9f2;
	}

	.bg-purple-dark {
		background: #99a9bf;
	}

	.container {
		width: 100%;

		.zhiWei {
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

		.fanyong {
			margin-bottom: 20rpx;
			margin-left: 20rpx;
			margin-right: 20rpx;
			margin-top: 30rpx;
			height: 360rpx;
			background-color: #fff;
			border-radius: 15px;

			.fanyong-head {
				width: 100%;

				.fanyong-tittle {
					height: 50rpx;
					font-size: 18px;
					font-weight: 1000;
					margin-top: 30rpx;
					padding-left: 20rpx;
					float: left;
				}

				.fanyong-tip {
					float: right;
					height: 50rpx;
					margin-top: 30rpx;
					padding-right: 20rpx;
				}
			}

			.fanyong-img {
				float: left;
				height: 200rpx;
				width: 100%;
				padding-top: 90rpx;

				.fanyong-money {
					color: #ffffff;
					font-size: 32rpx;
					margin-left: 60rpx;

					.onmoney {
						padding: 10rpx;
						font-size: 48rpx;
					}
				}

				.fanyong-tips {
					color: #ffffff;
					font-size: 20rpx;
					margin-left: 60rpx;
				}
			}

			.fanyong-jiesuan {
				float: left;
				width: 100%;
				padding-top: 30rpx;
				margin-left: 30rpx;
			}
		}

		.ganwei {
			margin-bottom: 20rpx;
			margin-left: 20rpx;
			margin-right: 20rpx;
			margin-top: 30rpx;
			/* #ifdef H5 */
			height: 1250px;
			/* #endif */
			/* #ifndef H5 */
			height: 1800rpx;
			/* #endif */
			background-color: #fff;
			border-radius: 15px;

			.ganwei-tittle {
				/* #ifdef H5 */
				height: 20px;
				/* #endif */
				/* #ifndef H5 */
				height: 50rpx;
				/* #endif */
				font-size: 18px;
				font-weight: 1000;
				margin-top: 30rpx;
				padding-left: 20rpx;
				float: left;
			}

			.ganwei-zhiwei {
				color: #ffaa00;
				width: 100%;
				/* #ifdef H5 */
				height: 30px;
				/* #endif */
				/* #ifndef H5 */
				height: 50rpx;
				/* #endif */
				font-size: 16px;
				font-weight: 1000;
				margin-top: 30rpx;
				padding-left: 20rpx;
				float: left;
			}

			.ganwei-info-fuli {
				width: 100%;
				/* #ifdef H5 */
				height: 200px;
				/* #endif */
				/* #ifndef H5 */
				height: 280rpx;
				/* #endif */
				font-size: 14px;
				margin-top: 30rpx;
				padding-left: 20rpx;
				float: left;

				.ganwei-info-tittle {
					width: 100%;
					/* #ifdef H5 */
					height: 30px;
					/* #endif */
					/* #ifndef H5 */
					height: 50rpx;
					/* #endif */
					font-size: 14px;
					font-weight: 1000;
					margin-top: 30rpx;
					padding-left: 20rpx;
				}
			}

			.ganwei-info-didian {
				width: 100%;
				/* #ifdef H5 */
				height: 290px;
				/* #endif */
				/* #ifndef H5 */
				height: 350rpx;
				/* #endif */
				font-size: 14px;
				margin-top: 30rpx;
				padding-left: 20rpx;
				float: left;

				.ganwei-info-tittle {
					width: 100%;
					/* #ifdef H5 */
					height: 50px;
					/* #endif */
					/* #ifndef H5 */
					height: 50rpx;
					/* #endif */
					font-size: 14px;
					font-weight: 1000;
					margin-top: 30rpx;
					padding-left: 20rpx;
				}
			}

			.ganwei-info-yaoqiu {
				width: 100%;
				/* #ifdef H5 */
				height: 480px;
				/* #endif */
				/* #ifndef H5 */
				height: 550rpx;
				/* #endif */
				font-size: 14px;
				margin-top: 30rpx;
				padding-left: 20rpx;
				float: left;

				.ganwei-info-tittle {
					width: 100%;
					/* #ifdef H5 */
					height: 50px;
					/* #endif */
					/* #ifndef H5 */
					height: 50rpx;
					/* #endif */
					font-size: 14px;
					font-weight: 1000;
					margin-top: 30rpx;
					padding-left: 20rpx;
				}
			}

			.ganwei-info-qiye {
				width: 100%;
				/* #ifdef H5 */
				height: 190px;
				margin-top: 30px;
				/* #endif */
				/* #ifndef H5 */
				height: 250rpx;
				margin-top: 30rpx;
				/* #endif */
				font-size: 14px;
				
				padding-left: 20rpx;
				float: left;

				.ganwei-info-tittle {
					width: 100%;
					/* #ifdef H5 */
					height: 30px;
					/* #endif */
					/* #ifndef H5 */
					height: 50rpx;
					/* #endif */
					font-size: 14px;
					font-weight: 1000;
					margin-top: 30rpx;
					padding-left: 20rpx;
				}
			}
		}
	}
</style>
