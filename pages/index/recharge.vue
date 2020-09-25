<template>
	<view class="view bgcColor fcolor">
		<view class="topimg">
			<view class="FY FX-sa" style="height: 100%;">
				<view class="FY FY-c">
					<text style="font-size: 38px;">{{endh}}:{{endm.toString().padStart(2, '0')}}:{{ends.toString().padStart(2, '0')}}</text>
					<text style="font-size: 14px;">time</text>
				</view>
				<view class="FX-sa" style="font-size: 14px;">
					<view class="FY FY-c">
						<text>{{andh}}:{{andm.toString().padStart(2, '0')}}:{{ands.toString().padStart(2, '0')}}</text>
						<text>开始</text>
					</view>
					<view class="FY FY-c">
						<text>{{stoph}}:{{stopm}}:{{stops.toString().padStart(2, '0')}}</text>
						<text>结束</text>
					</view>
				</view>
			</view>
		</view>
		
		<view class="bgcimg FY FY-c FX-c" v-if="bgcing">
			<view class="FY FY-c" type="default" @tap=start()>
				<image src="../../static/img/chongdian.png" mode=""></image>
				<text>{{state}}</text>
			</view>
		</view>
		<view class="bgcimg FY FY-c FX-c" v-else>
			<view class="FY FY-c" :class="sbool?'start':''" type="default" @tap=over()>
				<image :class="sbool?'stimg':''" src="../../static/img/chongdian.png" mode=""></image>
				<text class="por">{{state}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				testHour: 0,
				testMinute: 0,
				testSecond: 0,
				endh:'00',endm:'00',ends:'00',
				andh:'00',andm:'00',ands:'00',
				stoph:'00',stopm:'00',stops:'00',
				// endtime:'00:00:00',andtime:'00:00:00',stoptime:'00:00:00',
				bgcing:true,
				sbool:false,
				state:'开始',
				func:null,fund:null,
			}
		},
		created() {
			// setTimeout(() => {
			// 	this.testHour = 1
			// 	this.testMinute = 1
			// 	this.testSecond = 0
			// }, 2000)
			setInterval(()=>{
				let { s } = this
				s -- ;
				this.s = s
				if(this.s === 0 ){
					console.log("000")
				}
			},1000)
		},
		methods: {
			
			start(){
				this.sbool=true;
				this.bgcing=false;
				this.state='结束';
				this.endh='00';this.endm='00';this.ends='00';
				this.andh='00';this.andm='00';this.ands='00';
				var the =this;the.endm=30;
				the.func = setInterval(()=>{
					if(the.ends=='00'){
						the.ends=59;
						the.endm--;
					}else if(the.ends>0){
						the.ends--;
						console.log("秒数--");
					}
					if(the.endm==0&&the.ends==0){
						console.log('倒计时时间到');
						this.sbool=false;this.bgcing=true;this.state='开始';
						clearInterval(this.func);clearInterval(this.fund);
						this.stoph=this.andh;this.stopm=this.andm;this.stops=this.ands;
					}
				},1000);
				the.fund = setInterval(()=>{
					if(the.ands<59){
						the.ands++;
						console.log("秒数++");
					}else if(the.ands>=59){
						the.ands='00';
						the.andm++;
					}
					if(the.andm==30){
						console.log('计时时间到');
						clearInterval(this.func);clearInterval(this.fund);
						this.stoph=this.andh;this.stopm=this.andm;this.stops=this.ands;
					}
				},1000)
			},
			over(){
				this.sbool=false;
				this.bgcing=true;
				this.state='开始';
				this.stoph=this.andh;this.stopm=this.andm;this.stops=this.ands;
				clearInterval(this.func);
				clearInterval(this.fund);
			}
		}
	}
</script>

<style>
	.bgcColor{
		background-color: #1789E1!important;
		min-height: calc(100vh);
	}
	.topimg{
		height: calc(50vh);
	}
	.bgcimg{
		background: url(../../static/img/cdbottom.png) no-repeat;
		background-size:100% 100%;
		height: calc(50vh);
	}
	.bgcimg .FY{
		background-color: #FF834C;
		width: 40%;height: 40%;
		border-radius: 50%;
		padding: 2%;
	}
	.bgcimg image{
		width: 15%;
		height: 200rpx;
	}
	.start{
		transform:scale(.8,.8);
		transition:1s;
		animation: start 3s infinite linear;
	}
	.start .stimg{
		transform:scale(1.5,1.5);
		animation: stimg 3s infinite linear;
	}
</style>
