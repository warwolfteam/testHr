<template>
	<view class="container">
		<view class="home-search-area">
			<view class="city"
				@click="onCitySelect">{{currentCity}}</view>
			<u-search placeholder="搜索岗位任务"
				margin="15px"
				:show-action="fasle"
				:disabled="true"
				@click="openShowSearch">
			</u-search>
		</view>
		<u-sticky>
			<!-- 只能有一个根元素 -->
			<view class="classificationFiltering">
				<view class="lbotton">
					<u-button @click="onZongHeBotton"
						size="mini"
						:custom-style="zongHeBottonStyle">综合</u-button>
					<u-button @click="onZuiXineBotton"
						size="mini"
						:custom-style="zuiXinBottonStyle">最新</u-button>
				</view>
				<view class="rbotton">
					<u-button @click="onGanWeiBotton"
						size="mini"
						:custom-style="otherBottonStyle">岗位分类<u-icon name="grid"></u-icon>
					</u-button>
					<u-button @click="onShaiXuanBotton"
						size="mini"
						:custom-style="otherBottonStyle">筛选<u-icon name="grid"></u-icon>
					</u-button>
				</view>
			</view>
		</u-sticky>
		<!-- 以下为弹出层 -->
		<u-popup v-model="showSearch"
			mode="center"
			width="100%"
			height="100%">
			<view class="u-popup-search-area">
				<u-icon class="sIcon"
					@click="canceSearch"
					name="arrow-left"
					color="#2979ff"
					size="38"></u-icon>
				<u-search placeholder="搜索任务名称/用工企业"
					margin="20px"
					:show-action="fasle"
					v-model="keyword">
				</u-search>
			</view>
		</u-popup>
		<well-tree-select @doConfirm="doConfirmCategorys"
			:showDialog.sync="showGanWeiSelect"
			:data="ganWeiSelectList"
			:title-text="'选择职位'"
			:max-selected="1"
			:selected-values="ganWeiSelectedIds">
		</well-tree-select>
		<u-select v-model="showCitySelect"
			mode="mutil-column-auto"
			:list="cityList"
			@confirm="submitCitySelect"></u-select>
	</view>
</template>
<script>
	import wellTreeSelect from '@/components/well-treeSelect/well-treeSelect.vue';
	import zhiweidata from '@/common/zhiweidata.js'
	export default {
		components: {
			wellTreeSelect
		},
		data() {
			return {
				// 搜索框默认值
				keyword: "",
				// 弹出层判断条件
				// 显示搜索层
				showSearch: false,
				//显示城市选择层
				showCitySelect: false,
				showGanWeiSelect: false,
				// 城市显示默认值
				currentCity: "全国",
				bottonActive: true,
				// 按钮样式
				zongHeBottonStyle: {
					marginTop: '5rpx', // 注意驼峰命名，并且值必须用引号包括，因为这是对象
					marginBotton: '5rpx', // 注意驼峰命名，并且值必须用引号包括，因为这是对象 
					marginRight: '20rpx',
					color: 'blue'
				},
				zuiXinBottonStyle: {
					marginTop: '5rpx', // 注意驼峰命名，并且值必须用引号包括，因为这是对象
					marginBotton: '5rpx', // 注意驼峰命名，并且值必须用引号包括，因为这是对象 
					marginRight: '20rpx',
					color: 'blue'
				},
				otherBottonStyle: {
					marginTop: '5rpx', // 注意驼峰命名，并且值必须用引号包括，因为这是对象
					marginBotton: '5rpx', // 注意驼峰命名，并且值必须用引号包括，因为这是对象 
					marginRight: '20rpx',
					color: 'blue'
				},
				ganWeiSelectedIds: ['2-1-2'],
				ganWeiSelectList: zhiweidata.zhiweidata,
				cityList: [{
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
			openShowSearch() {
				this.showSearch = true;
			},
			canceSearch() {
				this.showSearch = false;
			},
			// 以下为点击按钮激活弹出层按钮
			onZongHeBotton() {
				console.log("点击综合按钮");
				this.zongHeBottonStyle.color = "red";
				this.zuiXinBottonStyle.color = "blue";
			},
			onZuiXineBotton() {
				console.log("点击最新按钮");
				this.zongHeBottonStyle.color = "blue";
				this.zuiXinBottonStyle.color = "red";
			},
			onGanWeiBotton() {
				console.log("点击岗位分类按钮");
				this.showGanWeiSelect = true;
				console.log("this.showGanWeiSelect:", this.showGanWeiSelect);
			},
			doConfirmCategorys(items) {
				let arr = [];
				for (let i = 0; i < items.length; i++) {
					arr.push(items[i].label);
				}
				this.selectedItemsStr = arr.join(',');
				console.log("doConfirmCategorys", this.selectedItemsStr);
			},
			onShaiXuanBotton() {
				console.log("点击筛选按钮");
			},
			onCitySelect() {
				console.log("点击切换城市按钮");
				this.showCitySelect = true;
			},
			submitCitySelect(e) {
				console.log("输出选择结果", e);
				console.log("输出选择结果名称", e[e.length - 1].label);
				this.currentCity = e[e.length - 1].label
			},
		}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #cccccc47;
		height: 200vh;

		// margin-top: 150rpx;
		.home-search-area {
			padding: 5rpx;
			display: flex;
			background-color: #fff;

			.city {
				align-self: center;
				font-size: 30rpx;
				margin-left: 10rpx;
			}
		}

		.classificationFiltering {
			width: 100%;
			height: 120rpx;
			background-color: #fff;
			color: #2979ff;
			padding: 8rpx;
			padding-top: 30rpx;

			// align-self: center;
			.lbotton {
				margin-left: 50rpx;
				float: left;
			}

			.rbotton {
				margin-right: 30rpx;
				float: right;
			}
		}

		// background-color: #ccc;
		.u-popup-search-area {
			padding: 30rpx;
			display: flex;

			.sIcon {
				align-self: center;
			}
		}
	}
</style>
