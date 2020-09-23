<template>
	<view class="view fcolor por">
		<view class="bgcimg">
				<view class="">
					<image class="imgl" src="../../static/img/树叶.png"></image>
					<view class="FY poa">
						<text>
							一杯好<text class="blocks t-center" style="width: 80rpx;height: 80rpx;background-color: #FF834C;border-radius: 50%;">水</text>
						</text>
						<text>一生健康</text>
					</view>
				</view>
				<image class="imgr" src="../../static/img/01.png" mode=""></image>
		</view>
		<view class="btn">
			<button class="bgcColor fcolor" type="default" @tap="over()">取消</button>
		</view>
		<view class="jishu bgcColor fcolor F-xy w30 poa">
			<!-- 倒计时{{endh}}:{{endm.toString().padStart(2, '0')}}:{{ends.toString().padStart(2, '0')}} -->
			倒计时{{timestr}}
		</view>
		<view class="zhezhao F-xy pof min-height min-width" v-if="kbool">
			<view class="kuang">
				<view class="" style="color: #999;font-size: 28px;" @tap="kuang()">
					×
				</view>
				<view class="FY FY-c f-bold" style="font-size: 18px;">
					恭喜您
					<text style="font-size: 16px;">免费获得一次次数的机会</text>
				</view>
				<view class="FX-c" style="margin: 8% 0;">
					<image style="width: 70%;height: 290rpx;" src="../../static/img/02.png" mode=""></image>
				</view>
				<button class="w50 fcolor bgcColor" type="default" @tap="kuang()">知道了</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				kbool:false,
				endh:'00',endm:'00',ends:'00',
				func:null,
				timestr:'00:00',
				totalSecond:70
			}
		},
		onLoad() {
			this.start();
		},
		methods: {
			kuang(){
				this.kbool=false;
			},
			start(){
				var the =this;
				var time = the.totalSecond;
				the.func = setInterval(()=>{
					time--;
					the.timestr=parseInt(time/60).toString().padStart(2, '0')+':'+(time%60).toString().padStart(2, '0');
					console.log(time);
					console.log("the",the.timestr);
					if(time==0){
						console.log('时间到');
						clearInterval(the.func);
						the.kbool=true;
					}
				},1000);
			},
			over(){
				clearInterval(this.func);
				uni.navigateBack({
					data:1
				})
			}
		}
	}
</script>

<style>
	.view{
		min-height: calc(100vh);
	}
	.bgcimg{
		min-height: calc(70vh);
		background: url(../../static/img/BG.png) no-repeat;
		background-size: 100% 100%;
		display: flex;
	}
	.bgcimg .poa{
		margin-top: 20%;
		margin-left: 10%;
		font-size: 26px;
	}
	.imgl{
		position: absolute;
		width: 70%;
		height: calc(30vh);
	}
	.imgr{
		position: relative;
		width: 25%;
		height: calc(35vh);
		right: -50%;
		top: 20rpx;
	}
	.btn{
		padding: 0 10%;
	}
	.btn .bgcColor{
		border-radius: 80rpx;
		font-size: 16px;
	}
	.jishu{
		height: 70rpx;
		right: 0;top: 3%;
		border-radius: 60rpx 0 0 60rpx;
		box-shadow: 0 0 10rpx #000000;
		box-sizing: border-box;
	}
	.zhezhao{
		top: 0;left: 0;
		color: #000000;
		background-color: rgba(102, 102, 102,.6);
	}
	.zhezhao .kuang{
		width: 80%;
		height: 60%;
		background-color: #fff;
		border-radius: 20rpx;
		padding: 2%;
		box-sizing: border-box;
	}
	.zhezhao .kuang button{
		margin-bottom: 5%;
		font-size: 12px;
		border-radius: 80rpx;
	}
</style>
