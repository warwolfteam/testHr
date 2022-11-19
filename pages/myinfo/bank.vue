<template>
	<view class="container">
		<view class="tittle"> 此银行账户将作为结算时您的收款账户，请填写正确 </view>
		<view class="bg">
			<view class="myinfo">
				<view class="myinfo-cell">
					<u-cell-group :border="false">
						<u-cell-item title="户名"
							:value="accountName"
							:border-top="false"
							:border-bottom="true"
							:arrow="true"
							@click="selectAccountName"></u-cell-item>
						<u-cell-item title="银行名称"
							:value="bankName"
							:border-top="false"
							:border-bottom="true"
							:arrow="true"
							@click="toEditInfo"></u-cell-item>
						<u-cell-item title="开户行省市"
							:value="bankCity"
							:border-top="false"
							:border-bottom="true"
							:arrow="true"
							@click="selectBankCity"></u-cell-item>
						<u-cell-item title="开户支行"
							:border-top="false"
							:border-bottom="true"
							:arrow="false"
							@click="toEditInfo">
							<u-input slot="right-icon"
								v-model="bankCityName"
								input-align="right"
								type="text"
								:border="false" />
						</u-cell-item>
						<u-cell-item title="银行账号"
							:border-top="false"
							:border-bottom="false"
							:arrow="false">
							<u-input slot="right-icon"
								v-model="bankCardNumber"
								input-align="right"
								type="text"
								:border="false" />
						</u-cell-item>
					</u-cell-group>
				</view>
			</view>
		</view>
		<u-select v-model="showBankCity"
			mode="mutil-column-auto"
			:list="bankCityList"
			@confirm="confirmBankCity"></u-select>
		<u-select v-model="showAccountName"
			mode="single-column"
			:list="accountNameList"
			@confirm="confirmAccountName"></u-select>
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	export default {
		components: {},
		data() {
			return {
				show: false,
				accountName: "江西某某科技公司",
				bankName: "台州银行",
				bankCity: "江西-赣州",
				bankCityName: "瑞金某某支行",
				bankCardNumber: "6400 01** ***0 015",
				showBankCity: false,
				showAccountName: false,
				accountNameList: [{
					value: '1',
					label: '江西某某公司'
				}],
				bankCityList: [{
					value: 1,
					label: '中国',
					children: [{
						value: 2,
						label: '广东',
						children: [{
							value: 3,
							label: '深圳'
						}, {
							value: 4,
							label: '广州'
						}]
					}, {
						value: 5,
						label: '广西',
						children: [{
							value: 6,
							label: '南宁'
						}, {
							value: 7,
							label: '桂林'
						}]
					}]
				}, {
					value: 8,
					label: '美国',
					children: [{
						value: 9,
						label: '纽约',
						children: [{
							value: 10,
							label: '皇后街区'
						}]
					}]
				}]
			}
		},
		methods: {
			toEditInfo() {
				console.log("点击解除与认证主体绑定");
			},
			selectBankCity() {
				console.log("点击开户行省市");
				this.showBankCity = true;
			},
			selectAccountName() {
				console.log("点击户名");
				this.showAccountName = true;
			},
			confirmBankCity(e) {
				console.log("点击开户行省市确定", e);
				console.log(e[0].label + "-" + e[1].label + "-" + e[2].label);
				this.bankCity = e[1].label + "-" + e[2].label;
			},
			confirmAccountName(e) {
				console.log("点击户名确定", e);
				console.log(e[0].label);
				this.accountName = e[0].label;
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

		.tittle {
			text-align: center;
			height: 80rpx;
			width: 100%;
			background-color: #f8ffb9;
			color: #ffaa00;
			font-size: 28rpx;
			line-height: 80rpx;
		}

		.bg {
			// background-color: #e7e7e7;
			padding-top: 30rpx;
			padding-bottom: 30rpx;

			.myinfo {
				background-color: #ffffff;
				padding: 30rpx;
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
