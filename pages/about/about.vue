<template>
	<view class="container">
		<view class="aboue-banner">
			<u-swiper :list="bannerlist"></u-swiper>
		</view>
		<u-card :border="false"
			padding="30"
			:foot-border-top="false">
			<view class=""
				slot="body">
				<view class="ucard u-flex">
					图灵优聘是金柚网的B2B数字化招聘平台，基于人工智能算法的人才画像、人岗匹配和AI面试等工具，助力企业构建规模化和个性化的招聘能力；同时，也通过技术赋能接单方，建立自己的品牌，便捷高效、灵活透明地做单，实现价值最大化。
				</view>
				<view class="ucard u-flex ">
					金柚网成立于2014年，是国内知名人力资源数字化服务商，全国布局155家自营分公司，400多家服务网点，遍及27个省、直辖市和自治区。依托金柚网深耕多年人力资源行业的积累与品牌沉淀，图灵优聘拥有遍布全国85000+行业名企的海量优质商机，涵盖餐饮、零售、物流、智能制造、金融、医药等行业的热门岗位。
				</view>
			</view>
		</u-card>
	</view>
</template>
<script>
	import homeData from '@/common/home-data.js'
	export default {
		components: {},
		data() {
			return {
				bannerlist: [{
					image: 'https://cdn.uviewui.com/uview/swiper/1.jpg'
				}, {
					image: 'https://cdn.uviewui.com/uview/swiper/2.jpg'
				}, {
					image: 'https://cdn.uviewui.com/uview/swiper/3.jpg'
				}],
			}
		},
		methods: {}
	}
</script>
<style lang="scss"
	scoped>
	.container {
		background-color: #ffffff47;

		.aboue-banner {
			padding: 40rpx;
			background-color: #ffffff47;
		}
	}

	.ucard {
		margin-top: 30rpx;
	}
</style>
