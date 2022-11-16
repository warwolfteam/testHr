<template>
	<div class="well-dialog"
		:class="{'well-dialog--show':showDialog }">
		<div class="well-dialog__mask"
			@click="closeDialog"></div>
		<div class="well-dialog__container">
			<div class="tree-select-contain">
				<div class="header">
					<div class="caption">
						{{titleText}}
					</div>
					<div class="action"
						@click="confirm()"> 确定 </div>
				</div>
				<scroll-view scroll-x
					style="width: 100%;height: 100%;"
					:scroll-left="scrollLeft"
					:scroll-with-animation="true">
					<div class="con">
						<div class="col">
							<scroll-view scroll-y
								style="height: 100%;">
								<ul>
									<li v-for="(item, index) in data"
										:key="index"
										@click="clickNavItem(index)"
										:class="{'active': activedNavIndex == index,'selected':item.selected}">
										{{item.label}}
									</li>
								</ul>
							</scroll-view>
						</div>
						<div class="col">
							<scroll-view scroll-y
								style="height: 100%;">
								<ul>
									<li v-for="(item, index) in colItems2"
										:key="index"
										@click="clickSubItem(index)"
										:class="{'active': activedSubIndex === index,'selected':item.selected}">
										{{item.label}}
									</li>
								</ul>
							</scroll-view>
						</div>
						<div class="col">
							<scroll-view scroll-y
								style="height: 100%;">
								<ul>
									<li v-for="(item, index) in colItems3"
										:key="index"
										@click="clickThirdItem(item,index)"
										:class="{'active': item.selected}">
										<div class="label-font">{{item.label}}</div>
										<icon type="success_no_circle"
											size="20"
											v-if="item.selected"
											color="#0083FF" />
									</li>
								</ul>
							</scroll-view>
						</div>
					</div>
				</scroll-view>
			</div>
		</div>
	</div>
</template>
<script>
	/**
	 * “分类选择器”组件
	 * 参数：
	 * @param showDialog 是否显示组件，true为打开
	 * @param titleText 组件标题
	 * @param maxSelected 最多选中几项
	 * @param selectedValues 选中的值的value，如：[060ef5006a504697a7d642d7e7d199cc', '060ef5006a504697a7d642d7e7d199cc']
	 * @param data 所要展示的数据，例子：
	 * [{
	 *     "label": "技术",
	 *      "children": [
	 *        {
	 *          "label": "后端开发"
	 *          "children": [
	 *             {
	 *               value: '060ef5006a504697a7d642d7e7d199cc',
	 *               label: 'Java'
	 *             },
	 *             {
	 *               value: '060ef5006a504697a7d642d7e7d199cc',
	 *               label: 'Java'
	 *             }]
	 *        }]
	 * }]
	 *
	 * 事件：
	 * @clickNav 点击一级标签时触发的事件
	 * @clickSub 点击二级标签时触发的事件
	 * @clickThird 点击三级标签时触发的事件
	 * @doConfirm 点击确定时触发的事件
	 *
	 *
	 * 例子：
	 * <well-tree-select @doConfirm="doConfirmCategorys"
	 *                   :showDialog.sync="showDialog"
	 *                   :data="categorysList"
	 *                   :title-text="'选择职位'"
	 *                   :max-selected="2"
	 *                   :selected-ids="selectedValues"></well-tree-select>
	 * **/
	export default {
		props: {
			showDialog: {
				type: Boolean,
				default: false
			},
			titleText: {
				type: String,
				default: '请选择'
			},
			data: {
				type: Array,
				default: []
			},
			maxSelected: {
				type: Number,
				default: 3
			},
			selectedValues: {
				type: Array,
				default: []
			}
		},
		data() {
			return {
				scrollLeft: 0,
				activedNavIndex: 0, //第一列选中第几个
				activedSubIndex: null, //第二列选中第几个
				colItems2: [], //第二列数据
				colItems3: [], //第三列数据
				selectedItems: [] //选中的数据
			};
		},
		watch: {
			selectedValues: {
				handler: function(newValue, oldValue) {
					console.log('selectedValues change', newValue);
					this.initChange();
				},
				immediate: true
			},
			data(newData, oldData) {
				console.log('newData');
				this.initChange();
			}
		},
		methods: {
			/**
			 * 点击遮罩层关闭弹窗
			 * **/
			closeDialog() {
				this.$emit('update:showDialog', false);
			},
			/**
			 * 点击第一列
			 * **/
			clickNavItem(index) {
				//console.log("clickNavItem");
				this.activedNavIndex = index;
				this.activedSubIndex = null;
				//更新第二列及第三列数据
				this.setColItems();
				this.$emit('clickNav', index);
			},
			/**
			 * 点击第二列
			 * **/
			clickSubItem(index) {
				this.activedSubIndex = index;
				console.log('clickSubItem', index);
				//更新第二列及第三列数据
				this.setColItems();
				this.scrollLeft = this.scrollLeft + wx.getSystemInfoSync().windowWidth / 2;
				this.$emit('clickSub', index);
			},
			/**
			 * 点击第三列
			 * **/
			clickThirdItem(item, index) {
				this.selectedItems.push({
					navIndex: this.activedNavIndex,
					subIndex: this.activedSubIndex,
					thirdIndex: index,
					value: item.value,
					label: item.label
				});
				//最多选择maxSelected项
				let delectCount = this.selectedItems.length - this.maxSelected;
				if (delectCount > 0) {
					this.selectedItems.splice(0, delectCount);
				}
				//selectedItems发生了变化，需要更新选中状态
				this.updateSelectedStyle();
				this.$emit('clickThird', item);
			},
			/**
			 * 点击确认
			 * **/
			confirm() {
				this.$emit('doConfirm', this.selectedItems);
				this.closeDialog();
			},
			/**
			 * 初始化选中状态
			 * **/
			initChange() {
				//根据外部出入的ids，找出每个选中值的上级下标
				let col1 = this.data || [];
				let flag = false;
				for (let i = 0; i < col1.length; i++) {
					let col2 = col1[i].children || [];
					for (let j = 0; j < col2.length; j++) {
						let col3 = col2[j].children || [];
						for (let k = 0; k < col3.length; k++) {
							if (this.selectedValues.indexOf(col3[k].value) > -1) {
								this.selectedItems.push({
									navIndex: i,
									subIndex: j,
									thirdIndex: k,
									value: col3[k].value,
									label: col3[k].label
								});
								if (!flag) {
									this.activedNavIndex = i;
									this.activedSubIndex = j;
									flag = true;
								}
							}
						}
					}
				}
				//根据选中值展示每列数据
				this.setColItems();
				//根据选中值，设置选中状态
				this.updateSelectedStyle();
			},
			/**
			 * 更新选中样式
			 * **/
			updateSelectedStyle() {
				//先取消所有选中状态
				let col1 = this.data || [];
				for (let i = 0; i < col1.length; i++) {
					col1[i].selected = false;
					let col2 = col1[i].children || [];
					for (let j = 0; j < col2.length; j++) {
						col2[j].selected = false;
						let col3 = col2[j].children || [];
						for (let k = 0; k < col3.length; k++) {
							col3[k].selected = false;
						}
					}
				}
				let _selects = this.selectedItems || [];
				for (let i = 0; i < _selects.length; i++) {
					let item = _selects[i];
					let col1 = this.data[item.navIndex];
					let col2 = col1.children[item.subIndex];
					let col3 = col2.children[item.thirdIndex];
					col1.selected = true;
					col2.selected = true;
					col3.selected = true;
				}
			},
			/**
			 * activedNavIndex、activedSubIndex发生变化时，
			 * 设置第二列和第三列数据
			 * **/
			setColItems: function() {
				let vm = this;
				let res2 = {};
				if (vm.activedNavIndex || vm.activedNavIndex === 0) {
					res2 = vm.data[vm.activedNavIndex] || {};
				}
				this.colItems2 = res2.children || [];
				let res3 = {};
				if (vm.activedSubIndex || vm.activedSubIndex === 0) {
					res3 = vm.colItems2[vm.activedSubIndex] || {};
				}
				this.colItems3 = res3.children || [];
			}
		},
		components: {},
		onShow() {},
		created() {}
	};
</script>
<style lang="less"
	scoped>
	@import './well-treeSelect.less';
</style>
