<template>
	<view class="view fcolor">
		<view class="bgcimg por FX-c">
			<view class="topimg poa">
				<text>123456789</text>
			</view>
		</view>
		<view class="btn FY-c">
			<button class="bgcColor fcolor" type="default">取消</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	.view{
		min-height: calc(100vh);
	}
	.bgcimg{
		min-height: calc(50vh);
		background-color: #1789E1;
	}
	.bgcimg .topimg{
		color: #000000;
		width: 90%;
		height: calc(60vh);
		background: url(../../static/img/shuizhi.png) no-repeat;
		background-size: 100% 100%;
		margin-top: 10%;
		padding: 4% 2%;
		box-sizing: border-box;
		font-size: 16px;
	}
	.btn{
		min-height: calc(50vh);
		margin-top: 20%;
	}
	.btn .bgcColor{
		width: 90%;
		border-radius: 80rpx;
		font-size: 16px;
	}
</style>
