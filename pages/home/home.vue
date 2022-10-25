<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in bannerList" :key="item.goods_id">
				<img :src="item.image_src" alt="">
			</swiper-item>
		</swiper>
		<ul>
			<li v-for="(item,index) in navList" :key="index">
				<img :src="item.image_src" alt="">
			</li>
		</ul>
	</view>
</template>

<script>
	import {
		mapState
	} from 'vuex';
	export default {
		data() {
			return {
				bannerList: [],
				navList: [],
				floorList: []
			};
		},
		methods: {
			async getbannerList() {
				let {
					data: res
				} = await uni.$http.get('home/swiperdata')
				// console.log(res);
				this.bannerList = res.message
			},
			async getnavList() {
				let {
					data: res
				} = await uni.$http.get('home/catitems')
				// console.log(res);
				this.navList = res.message
			},
			async getfloorList() {
				let {
					data: res
				} = await uni.$http.get('home/floordata')
				console.log(res);
			}
		},
		mounted() {
			this.getbannerList()
			this.getnavList()
			this.getfloorList()
		}
	}
</script>

<style lang="scss">
	swiper {
		width: 100%;
		height: 400rpx;

		img {
			width: 100%;
			height: 400rpx;
		}
	}

	ul {
		display: flex;
		justify-content: space-between;
		padding: 20rpx;

		img {
			width: 160rpx;
			height: 160rpx;
		}
	}
</style>
