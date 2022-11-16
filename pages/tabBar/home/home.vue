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
						:custom-style="otherBottonStyle">岗位分类<u-icon size="30"
							name="grid"></u-icon>
					</u-button>
					<u-button @click="onShaiXuanBotton"
						size="mini"
						:custom-style="otherBottonStyle">筛选<u-icon size="30"
							name="calendar"></u-icon>
					</u-button>
				</view>
			</view>
		</u-sticky>
		<z-zhiwei-list :dataList="zZhiweiData"></z-zhiwei-list>
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
			<view class="u-popup-search-body">
				<z-zhiwei-list :dataList="zZhiweiData"></z-zhiwei-list>
			</view>
		</u-popup>
		<well-tree-select @doConfirm="doConfirmCategorys"
			:showDialog.sync="showGanWeiSelect"
			:data="ganWeiSelectList"
			:title-text="'选择职位'"
			:max-selected="1"
			:selected-values="ganWeiSelectedIds">
		</well-tree-select>
		<u-popup v-model="showShaiXuan"
			mode="center"
			width="100%"
			height="100%">
			<view class="u-popup-shaiXuan-area">
				<view class="sIcon">
					<u-icon @click="canceShaiXuan"
						name="arrow-left"
						color="#2979ff"
						size="38"></u-icon>
				</view>
				<view class="s-shaiXuan-body">
					<view class="box-area-body">
						<p class="p-title">结算方式</p>
						<view class="box-area">
							<u-checkbox-group @change="shaiXuanCheckboxGroupChange"
								max="1">
								<u-checkbox @change="shaiXuanCheckboxChange"
									v-model="item.checked"
									v-for="(item, index) in shaiXuanJieSuanList"
									:key="index"
									:name="item.name">{{item.name}}</u-checkbox>
							</u-checkbox-group>
						</view>
					</view>
					<view class="box-area-body">
						<p class="p-title">需求人数</p>
						<view class="box-area">
							<u-checkbox-group @change="shaiXuanCheckboxGroupChange"
								max="1">
								<u-checkbox @change="shaiXuanCheckboxChange"
									v-model="item.checked"
									v-for="(item, index) in shaiXuanXuQiuList"
									:key="index"
									:name="item.name">{{item.name}}</u-checkbox>
							</u-checkbox-group>
						</view>
					</view>
					<view class="box-area-body">
						<p class="p-title">任务亮点</p>
						<view class="box-area">
							<u-checkbox-group @change="shaiXuanCheckboxGroupChange">
								<u-checkbox @change="shaiXuanCheckboxChange"
									v-model="item.checked"
									v-for="(item, index) in shaiXuanRenWuList"
									:key="index"
									:name="item.name">{{item.name}}</u-checkbox>
							</u-checkbox-group>
						</view>
					</view>
					<view class="box-area-body">
						<p class="p-title">岗位薪酬</p>
						<view class="box-input">
							<u-input placeholder="自定最低薪酬"
								v-model="lowMoney"
								type="number"
								border="true" />
							<p class="p-line">--</p>
							<u-input placeholder="自定最高薪酬"
								v-model="highMoney"
								type="number"
								border="true" />
						</view>
						<view class="box-area">
							<u-checkbox-group @change="shaiXuanCheckboxGroupChange"
								max="1">
								<u-checkbox @change="shaiXuanCheckboxChange"
									v-model="item.checked"
									v-for="(item, index) in shaiXuanGanWeiList"
									:key="index"
									:name="item.name">{{item.name}}</u-checkbox>
							</u-checkbox-group>
						</view>
					</view>
				</view>
				<view class="s-shaiXuan-button">
					<u-button @click="shaiXuanCheckedSubmit">确定</u-button>
				</view>
			</view>
		</u-popup>
		<u-select v-model="showCitySelect"
			mode="mutil-column-auto"
			:list="cityList"
			@confirm="submitCitySelect"></u-select>
	</view>
</template>
<script>
	import wellTreeSelect from '@/components/well-treeSelect/well-treeSelect.vue';
	import zZhiweiList from '@/components/z-zhiwei-list/z-zhiwei-list.vue'
	import homeData from '@/common/home-data.js'
	export default {
		components: {
			wellTreeSelect,
			zZhiweiList
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
				showShaiXuan: false,
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
				ganWeiSelectList: homeData.zhiweidata,
				lowMoney: "",
				highMoney: "",
				shaiXuanJieSuanList: homeData.shaiXuanJieSuanList,
				shaiXuanXuQiuList: homeData.shaiXuanXuQiuList,
				shaiXuanRenWuList: homeData.shaiXuanRenWuList,
				shaiXuanGanWeiList: homeData.shaiXuanGanWeiList,
				cityList: homeData.cityList,
				zZhiweiData: homeData.zZhiweiData.data.list,
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
				this.showShaiXuan = true;
			},
			canceShaiXuan() {
				this.showShaiXuan = false;
			},
			// 选中某个复选框时，由checkbox时触发
			shaiXuanCheckboxChange(e) {
				console.log(e);
			},
			// 选中任一checkbox时，由checkbox-group触发
			shaiXuanCheckboxGroupChange(e) {
				console.log(e);
			},
			// 提交选项
			shaiXuanCheckedSubmit() {
				this.canceShaiXuan();
				console.log("点击确定按钮");
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

		.u-popup-search-body {
			padding: 10rpx;
			background-color: #cccccc47;
		}

		.u-popup-shaiXuan-area {
			padding: 10rpx;

			.sIcon {
				height: 130rpx;
			}

			.s-shaiXuan-body {
				margin: 20rpx;

				.box-area-body {
					margin-top: 20rpx;

					.p-title {
						margin-top: 10rpx;
					}

					.box-input {
						margin-top: 30rpx;
						display: flex;

						.p-line {
							width: 50rpx;
							margin: 20rpx;
						}
					}

					.box-area {
						margin-top: 20rpx;
					}
				}
			}

			.s-shaiXuan-button {
				margin-top: 200rpx;
			}
		}
	}
</style>
