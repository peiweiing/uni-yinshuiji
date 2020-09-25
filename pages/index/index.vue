<template>
	<view class="step">
		<view class="header">
			<view class="header_title">共享饮水机</view>
			<view class="image_box">
				<image src="../../static/index/header.png"></image>
			</view>
		</view>
		<view class="map">
			<map
				style="width: 100%; height: 600rpx;"
				:latitude="latitude"
				:longitude="longitude"
				:markers="markers"
				:scale="scale"
				show-location=true
				@markertap="labeltap"
				@labeltap="labeltap"
			></map>
		</view>
		<scroll-view scroll-y class="place">
			<view class="place_content">
				<view class="place_content_title">
					<text style="flex: 1; box-sizing: border-box; border-right: 2rpx solid #EEE;">位置</text>
					<text style="width: 20%;" @click="nav">距离</text>
				</view>
				<view class="place_content_list" v-for="(item, index) in waterInfo" :key="index">
					<view class="place_content_list_left">
						<image src="../../static/index/weizhi.png"></image>
					</view>
					<view class="place_content_list_center">
						<view style="font-size: 36rpx; color: #198AE3;">{{item.name}}</view>
						<view style="font-size: 28rpx; color: #8A8A8A;">{{item.address}}</view>
					</view>
					<view class="place_content_list_right">
						<image src="../../static/index/juli.png"></image>
						<text>{{`${item.distance}km`}}</text>
					</view>
				</view>
			</view>
			<button type="default" style="margin: 6rpx 40rpx;" @click="nav('../step/step')">取水</button>
			<button type="default" style="margin: 6rpx 40rpx;" @click="nav('./present')">当前状态</button>
			<button type="default" style="margin: 6rpx 40rpx;" @click="nav('./recharge')">充电</button>
			<button type="default" style="margin: 6rpx 40rpx;" @click="nav('./report')">检测报告</button>
			<button type="default" style="margin: 6rpx 40rpx;" @click="nav('./advertising')">广告</button>
		</scroll-view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			title: 'map',
			latitude: 34.331473,
			longitude: 108.949347,
			scale: 16,
			waterInfo: [
				{
					name: '西安MAX大厦饮水机',
					address: '西安市未央区',
					distance: 1.21
				},
				{
					name: '西安MAX大厦饮水机',
					address: '西安市未央区',
					distance: 2.21
				},
				{
					name: '西安MAX大厦饮水机',
					address: '西安市未央区',
					distance: 3.21
				}
			],
			markers: [
				{
					id: 0,
					latitude: 34.331473,
					longitude: 108.949347,
					width: '61rpx',
					height: '72rpx',
					iconPath: '../../static/index/tip.jpg',
					label: {
						content: '我的位置',
						color: '#333',
						fontSize: 14,
						borderWidth: 2,
						borderColor: '#999',
						borderRadius: 4,
						bgColor: '#FFF',
						padding: 5,
						textAlign: 'center'
					}
				},
				{
					id: 1,
					latitude: 34.332473,
					longitude: 108.949347,
					width: '61rpx',
					height: '72rpx',
					iconPath: '../../static/index/tip.jpg',
					label: {
						content: '未央区', // 文本
						color: '#333', // 文本颜色
						fontSize: 14, // 文字大小
						borderWidth: 2, // 边框宽度
						borderColor: '#999', // 边框颜色
						borderRadius: 4, // 边框圆角
						bgColor: '#FFF', // 背景色
						padding: 5, // 文本边缘留白
						textAlign: 'center' // 文本对齐方式
					}
				},
				{
					id: 2,
					latitude: 34.330473,
					longitude: 108.950347,
					width: '61rpx',
					height: '72rpx',
					iconPath: '../../static/index/tip.jpg',
					label: {
						content: '未央区',
						color: '#333',
						fontSize: 14,
						borderWidth: 2,
						borderColor: '#999',
						borderRadius: 4,
						bgColor: '#FFF',
						padding: 5,
						textAlign: 'center'
					}
				},
				{
					id: 3,
					latitude: 34.330073,
					longitude: 108.948347,
					width: '61rpx',
					height: '72rpx',
					iconPath: '../../static/index/tip.jpg',
					label: {
						content: '未央区',
						color: '#333',
						fontSize: 14,
						borderWidth: 2,
						borderColor: '#999',
						borderRadius: 4,
						bgColor: '#FFF',
						padding: 5,
						textAlign: 'center'
					}
				}
			]
		}
	},
	onLoad: function() {
		var _this = this;
		uni.getLocation({
			type: 'gcj02',
			success: function (res) {
				_this.latitude = res.latitude;
				_this.markers[0].latitude = res.latitude;
				_this.longitude = res.longitude;
				_this.markers[0].longitude = res.longitude;
		    }
		});
	},
	methods: {
		labeltap: function(e) {
			this.markers.forEach((item) => {
				if (item.id === e.markerId && e.markerId !== 0) {
					if (item.label.content.length > 5) {
						item.label.content = '未央区';
					} else {
						item.label.content = '未央区凤城五路地铁口\r\nMax未来13楼团团云科技';
					};
					return;
				}
			})
		},
		nav: function(url) { uni.navigateTo({ url }) }
	}
}
</script>

<style lang="scss" scoped>
	.step{
		position: absolute;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		background-color: #EEE;
		box-sizing: border-box;
	}
	.header{
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		height: 130rpx;
		.image_box{
			position: absolute;
			top: 0;
			bottom: 0;
			left: 0;
			right: 0;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.header_title{
			z-index: 999;
			position: absolute;
			bottom: 0;
			left: 0;
			right: 0;
			line-height: 88rpx;
			text-align: center;
			font-size: 32rpx;
			font-weight: bold;
			color: #FFF;
		}
	}
	.map{
		position: absolute;
		top: 20+130rpx;
		left: 0;
		right: 0;
	}
	.place{
		position: absolute;
		top: 640+130rpx;
		bottom: 0;
		left: 0;
		right: 0;
		background-color: #FFF;
		box-sizing: border-box;
		.place_content{
			margin: 20rpx;
			box-sizing: border-box;
			border-radius: 8rpx;
			border: 2rpx solid #EEE;
			.place_content_title{
				display: flex;
				font-size: 32rpx;
				line-height: 66rpx;
				box-sizing: border-box;
				border-bottom: 2rpx solid #EEE;
				text-align: center;
			}
			.place_content_list{
				display: flex;
				font-size: 32rpx;
				padding: 20rpx 0;
				box-sizing: border-box;
				border-bottom: 2rpx solid #EEE;
				.place_content_list_left{
					width: 14%;
					display: flex;
					justify-content: center;
					align-items: center;
					image{
						width: 41rpx;
						height: 44rpx;
					}
				}
				.place_content_list_center{
					flex: 1;
					display: flex;
					flex-direction: column;
					justify-content: center;
					box-sizing: border-box;
					border-right: 2rpx solid #EEE;
				}
				.place_content_list_right{
					width: 20%;
					font-size: 0;
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;
					image{
						width: 38rpx;
						height: 38rpx;
						margin-bottom: 10rpx;
					}
					text{
						font-size: 28rpx;
						color: #333;
					}
				}
			}
		}
	}
</style>