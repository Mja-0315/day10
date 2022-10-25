<template>
	<view style="margin-bottom: 200rpx;">
		<nav>
			<h1>天使童装</h1><input type="text" placeholder="输入关键字搜索">
		</nav>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in bannerList" :key="index">
				<img :src="item.picUrl" alt="">
			</swiper-item>
		</swiper>
		<ul class="ul1">
			<li>上装</li>
			<li>裤装</li>
			<li>特价区</li>
			<li>裙装</li>
			<li>套装</li>
			<li>外套</li>
			<li>秒杀</li>
			<li>内裤</li>
			<li>袜子</li>
			<li>鞋</li>
		</ul>
		<aside>
			<h1>优惠<span>资讯</span></h1>
			<p>商城新开张，优惠多多，戳 戳 <uni-icons type="forward" size="20" color="orange"></uni-icons>
			</p>
		</aside>
		<article>
			<h1>
				<uni-icons type="fire-filled" size="20" color="#f84947"></uni-icons> 爆品推荐
			</h1>
			<ul class="ul2">
				<li v-for="(item,index) in list.result" :key="index">
					<img :src="item.pic" alt="">
					<h1>{{item.name}}</h1>
					<p>{{item.characteristic}}</p>
					<h2>￥{{item.minPrice}}<span>￥{{item.originalPrice}}</span></h2>
				</li>
			</ul>
		</article>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				bannerList: [],
				list: [],
			};
		},
		methods: {
			async getbannerList() {
				let {
					data: res
				} = await uni.$http.get('banner/list')
				// console.log(res);
				this.bannerList = res.data
			},
			async getList() {
				let {
					data: res
				} = await uni.$http.post('shop/goods/list/v2')
				console.log(res);
				this.list = res.data
			}
		},
		mounted() {
			this.getbannerList()
			this.getList()
		}
	}
</script>

<style lang="scss">
	nav {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 20rpx;

		h1 {
			font-weight: 700;
			font-size: 40rpx
		}

		input {
			background-color: #f7f8fa;
			border: 1px solid #fff;
			width: 480rpx;
			height: 60rpx;
			border-radius: 16rpx;
		}
	}

	.ul1 {
		width: 88%;
		margin: auto;
		height: 360rpx;
		border-radius: 20rpx;
		display: flex;
		justify-content: space-between;
		align-items: flex-end;
		padding: 30rpx;
		flex-wrap: wrap;
		background-color: #fff;

		li {
			width: 20%;
			text-align: center;
			font-weight: 700;
		}
	}

	swiper {
		width: 100%;
		height: 400rpx;

		img {
			width: 100%;
			height: 100%;
		}
	}

	aside {
		display: flex;
		padding: 20rpx;
		justify-content: space-between;
		align-items: center;
		margin-top: 20rpx;
		margin-bottom: 40rpx;
		background-color: #fff;

		h1 {
			font-weight: 700;
			font-size: 40rpx;

			span {
				color: #ef8988;
			}
		}

		p {
			color: orange;
		}
	}

	article {
		background-color: #fff;
		padding: 30rpx;

		h1 {
			font-size: 40rpx;
			font-weight: 700;
			text-align: center;
		}

		ul {
			display: flex;
			justify-content: space-between;
			flex-wrap: wrap;
			margin-top: 30rpx;

			li {
				width: 48%;
				height: 540rpx;
				border: 2px solid #ccc;
				border-radius: 10rpx;
				margin-bottom: 20rpx;

				img {
					width: 100%;
					height: 65%;
				}

				h1 {
					font-size: 30rpx;
					text-align: left;
					padding-left: 20rpx;

				}

				p {
					color: #999;
					font-size: 24rpx;
					margin: 10rpx 0;
					padding-left: 20rpx;
				}

				h2 {
					font-weight: 700;
					font-size: 36rpx;
					color: #f10429;
					padding-left: 20rpx;

					span {
						color: #999;
						font-size: 24rpx;
						margin-left: 10rpx;
						font-style: initial;
					}
				}
			}
		}
	}
</style>
