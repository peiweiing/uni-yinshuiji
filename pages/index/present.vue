<template>
	<view class="view fcolor">
		<view class="topimg">
			<view class="top por FX-c">
				<text class="poa f-bold" style="color:#1789E0;top: 35%;left: 48%;z-index: 9;font-size: 16px;">优</text>
				<image src="../../static/img/shuidi.png" mode=""></image>
				<text class="poa" style="color:#1789E0;bottom: 35%;left: 43%;z-index: 9;">纯水水质</text>
			</view>
			<view class="cent boxcolor">
				<view class="cent-top FY-c">
					<image style="margin-right: 1%;" src="../../static/img/icon.png" mode=""></image>当前状态
				</view>
				<view class="FX-sa">
					<view class="FY FY-c">
						<text>99%</text>
						<text>滤芯寿命</text>
					</view>
					<view class="FY FY-c">
						<text>60%</text>
						<text>水温</text>
					</view>
					<view class="FY FY-c">
						<text>70%</text>
						<text>水量</text>
					</view>
				</view>
			</view>
			<view class="FX-c">
				<button class="end boxcolor" type="default" @tap="report()">水质报告</button>
			</view>
		</view>
		
		<view class="endimg FX-sa FY-c">
			<view class="endcs FY F-xy boxcolor" type="default">
				<text>取水</text>
				<text style="color: #999;">剩余{{shui}}(次)</text>
			</view>
			<view class="endcs FY F-xy boxcolor" type="default" @tap='recharge()'>
				<text>充电</text>
				<text style="color: #999;">剩余{{dian}}(次)</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				shui:1,
				dian:1
			}
		},
		methods: {
			report(){
				uni.navigateTo({
					url:'report'
				})
			},
			recharge(){
				uni.navigateTo({
					url:'recharge'
				})
			}
		}
	}
</script>

<style>

	.bgcColor{
		min-height: calc(100vh);
	}
	.topimg{
		height: calc(60vh);
		background: url(../../static/img/bgcimg.png) no-repeat;
		background-size: 200% 80%;
		animation: topimg 15s infinite linear;
	}
	.topimg .top{
		height: calc(40vh);
		padding-top: 5%;
		animation: image 5s infinite linear;
	}
	.topimg .top image{
		width: 220rpx;height: 380rpx;
	}
	.topimg .cent{
		color: #1789E0;
		background-color: #fff;
		margin: 0 10% 10%;
		padding: 4%;
		border-radius: 20rpx;
	}
	.topimg .cent-top{
		margin-bottom: 2%;
	}
	.topimg .cent .cent-top image{
		width: 50rpx;height: 50rpx;
	}
	.topimg .end{
		font-size: 12px;
		width: 55%;
		color: #fff;
		background-color: #1789E0;
		padding: 0;
		border-radius: 80rpx;
	}
	.topimg .end:hover,.topimg .end:target{
		transition: .5s;
		background-color: #1aa0ff;
	}
	.endimg{
		height: calc(40vh);
		padding: 10% 0 0;
		box-sizing: border-box;
	}
	.endimg .endcs{
		font-size: 14px;
		width: 240rpx;
		height: 110rpx;
		border-radius: 80rpx;
	}
	.endimg .endcs:hover,.endimg .endcs:target{
		transform: scale(.8,.8);
		transition: 1s;
		box-shadow: 0 0 40rpx #FF834C;
	}
	.endimg view:first-child{
		color: #000;
		border: 1px solid #FF834C;
	}
	.endimg view:last-child{
		color: #FFF;
		background-color: #FF834C;
	}
</style>
