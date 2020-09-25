<template>
	<view class="step">
		<view class="header">
			<view class="header_title">{{header}}</view>
			<view class="image_box">
				<image src="../../static/index/header.png"></image>
			</view>
		</view>
		<view class="progress">
			<tui-steps
				:items="items"
				:type="2"
				spacing="120rpx"
				activeColor="#198AE3"
				:titleSize='24'
				lineStyle='dashed'
				:activeSteps="activeSteps"
			></tui-steps>
		</view>
		<view class="tui-banner-box">
			<swiper
				indicator-dots="true"
				indicator-color="#CBDFFC"
				indicator-active-color="#478DF3"
				interval="800"
				:current="current"
				:autoplay="autoplay"
				class="tui-banner-swiper"
				@change="change"
			>
				<swiper-item class="tui-banner-item">
					<view class="banner_img ldx ldx_pulse" style="margin-top: 20rpx;">
						<image src="../../static/progress/01.png" style="width: 401rpx; height: 349rpx;"></image>
					</view>
					<view class="banner_info">
						<view class="banner_info1">
							<view class="banner_info_left">
								<image src="../../static/progress/shuiwen.png"></image>
							</view>
							<view class="banner_info_right">
								<view class="banner_info_right_top">水温(℃)</view>
								<view class="banner_info_right_bottom">
									<text @click="temperature(40)" :style="temp === 40 ? 'color: #FF834C; border-color: #FF834C;' : ''">40℃</text>
									<text @click="temperature(60)" :style="temp === 60 ? 'color: #FF834C; border-color: #FF834C;' : ''">60℃</text>
									<text @click="temperature(80)" :style="temp === 80 ? 'color: #FF834C; border-color: #FF834C;' : ''">80℃</text>
								</view>
							</view>
						</view>
						<view class="banner_info2">
							<view class="banner_info_left">
								<image src="../../static/progress/shuiliang.png"></image>
							</view>
							<view class="banner_info_right">
								<view class="banner_info_right_top">水量(ml)</view>
								<view class="banner_info_right_bottom">
									<text @click="milliliter(80)" :style="ml === 80 ? 'color: #FF834C; border-color: #FF834C;' : ''">80ml</text>
									<text @click="milliliter(100)" :style="ml === 100 ? 'color: #FF834C; border-color: #FF834C;' : ''">100ml</text>
									<text @click="milliliter(120)" :style="ml === 120 ? 'color: #FF834C; border-color: #FF834C;' : ''">120ml</text>
								</view>
							</view>
						</view>
						<view class="confirm ldx" :class="ldx_bounceIn" style="margin-top: 40rpx;" @click="confirm">完成</view>
					</view>
				</swiper-item>
				<swiper-item class="tui-banner-item">
					<view class="banner_img" style="margin-top: 160rpx;">
						<image class="ldx ldx_bounce" src="../../static/progress/001.png" style="width: 165rpx; height: 485rpx; margin-right: 40rpx;"></image>
						<image src="../../static/progress/02.png" style="width: 148rpx; height: 483rpx;"></image>
					</view>
					<view class="ldx ldx_pulse" style="margin-top: 130rpx; color: #198AE3; text-align: center;">请等待开门...</view>
				</swiper-item>
				<swiper-item class="tui-banner-item">
					<view class="banner_img ldx ldx_rubberBand">
						<image src="../../static/progress/03.png" style="width: 456rpx; height: 505rpx;"></image>
					</view>
					<view class="ldx ldx_pulse" style="margin-top: 200rpx; color: #198AE3; text-align: center;">请放置好您的水杯...</view>
				</swiper-item>
				<swiper-item class="tui-banner-item">
					<view class="banner_img ldx ldx_jello">
						<image src="../../static/progress/04.png" style="width: 381rpx; height: 521rpx;"></image>
					</view>
					<view class="ldx ldx_pulse" style="margin-top: 200rpx; color: #198AE3; text-align: center;">请稍作等待 马上就好...</view>
				</swiper-item>
				<swiper-item class="tui-banner-item">
					<view class="banner_img">
						<image class="ldx ldx_tada" src="../../static/progress/001.png" style="width: 165rpx; height: 485rpx;"></image>
						<image src="../../static/progress/05.png" style="width: 381rpx; height: 521rpx;"></image>
					</view>
					<view class="ldx ldx_pulse" style="margin: 80rpx 0 -20rpx; color: #198AE3; text-align: center;">请慢用哦...</view>
					<view class="banner_bottom">
						<view class="confirm ldx" :class="ldx_bounceIn" @click="confirm2">完成</view>
					</view>
				</swiper-item>
			</swiper>
		</view>
		<view class="bottom_backimg">
			<image src="../../static/progress/back.png"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				header: '取水',
				items: [
					{ title: "取水" },
					{ title: "等待开门" },
					{ title: "请放小杯" },
					{ title: "正在出水" },
					{ title: "请取走水杯" }
				],
				activeSteps: 0,
				current: 0,
				autoplay: false,
				temp: 40,
				ml: 80,
				// 按钮动画
				ldx_bounceIn: '',
				// 标记(用以控制函数触发频率)
				flag: 0,
			}
		},
		methods: {
			// swiper切换
			change: function(e) {
				const index = e.detail.current;
				if (this.current < index) {
					this.activeSteps = this.activeSteps + 1;
				} else {
					this.activeSteps = this.activeSteps - 1;
				};
				this.current = index;
				this.header = this.items[index].title;
			},
			// 按钮操作
			confirm: function() {
				if (this.flag === 0) {
					this.flag = 1;
					this.ldx_bounceIn = 'ldx_bounceIn';
					this.autoplay = true;
					setTimeout(() => {
						this.autoplay = false;
						this.ldx_bounceIn = '';
						this.flag = 0;
					}, 1000);
				};
			},
			// 按钮操作
			confirm2: function() {
				if (this.flag === 0) {
					this.flag = 1;
					this.ldx_bounceIn = 'ldx_bounceIn';
					setTimeout(() => {
						this.ldx_bounceIn = '';
						this.flag = 0;
					}, 1000);
				};
			},
			// 温度选择
			temperature: function(data) {
				this.temp = data;
				console.log(data);
			},
			// 温度选择
			milliliter: function(data) {
				this.ml = data;
				console.log(data);
			}
		}
	}
</script>

<style lang="scss" scoped>
	.step{
		box-sizing: border-box;
		position: absolute;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
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
	.progress{
		margin-top: 150rpx;
		width: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		box-sizing: border-box;
	}
	.tui-banner-box{
		width: 100%;
		height: 82%;
		box-sizing: border-box;
	}
	.tui-banner-swiper{
		width: 100%;
		height: 100%;
		box-sizing: border-box;
	}
	.tui-banner-item{
		box-sizing: border-box;
	}
	.banner_img{
		width: 100%;
		margin-top: 70rpx;
		text-align: center;
	}
	.banner_info{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 100%;
		.banner_info1, .banner_info2{
			display: flex;
			margin-top: 20rpx;
			width: 70%;
			padding: 10rpx 0;
			box-sizing: border-box;
			box-shadow: 0rpx 0rpx 10rpx #E0E0E0;
		}
		.banner_info_left{
			width: 80rpx;
			height: 80rpx;
			padding: 0 20rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.banner_info_right_top{
			font-size: 40rpx;
			line-height: 80rpx;
			color: #1D8DE2;
		}
		.banner_info_right_bottom{
			font-size: 40rpx;
			line-height: 80rpx;
			color: #1D8DE2;
			text{
				margin-right: 20rpx;
				box-sizing: border-box;
				border-bottom: 2rpx solid #1D8DE2;
			}
		}
	}
	.banner_bottom{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.confirm{
		margin-top: 100rpx;
		width: 140rpx;
		height: 140rpx;
		font-size: 50rpx;
		line-height: 140rpx;
		text-align: center;
		color: #FFF;
		box-sizing: border-box;
		border-radius: 50%;
		background-color: #FF834C;
	}
	.bottom_backimg{
		z-index: -999;
		position: absolute;
		bottom: 0;
		width: 100%;
		font-size: 0;
		image{
			width: 100%;
		}
	}
</style>
