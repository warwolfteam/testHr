<template>
	<view class="container">
		<view class="home-search-area">
			<!-- <u-icon class="quanguo"
				@click="canceSearch"
				name="arrow-left"
				color="#2979ff"
				size="38"></u-icon> -->
			<view class="city">{{currentCity}}</view>
			<u-search placeholder="搜索岗位任务"
				margin="15px"
				:show-action="fasle"
				:disabled="true"
				@click="openShowSearch">
			</u-search>
		</view>
		<view class="classificationFiltering">
		</view>
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
		<!-- <u-button @click="showSearch = true">打开</u-button> -->
	</view>
</template>
<script>
	export default {
		data() {
			return {
				navTittle: "首页",
				keyword: "",
				showSearch: false,
				currentCity: "全国"
			}
		},
		methods: {
			openShowSearch() {
				this.showSearch = true;
			},
			canceSearch() {
				this.showSearch = false;
			}
		}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #fff;

		.home-search-area {
			padding: 5rpx;
			display: flex;

			.city {
				align-self: center;
				font-size: 30rpx;
				margin-left: 10rpx;
			}
		}

		.classificationFiltering {}

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
