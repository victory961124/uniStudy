<template>
	<view>
		<!-- <view class="box" hover-class="box-hover animated rubberBand" 
		hover-start-time="50" hover-stay-time="800">测试文字</view> -->
		<view class="box">
			<view>1</view>
			<view>2</view>
			<view>3</view>
			<view>4</view>
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
.box{
	width: 300rpx;
	height: 300rpx;
	background-color: blue;
	margin: 100rpx;
	color: #FFFFFF;
}
.box>view{
	font-size: 40rpx;
}
.box>view:nth-of-type(2n-1){
	background-color: #09BB07;
}
.box>view:nth-of-type(2n){
	background-color: #333333;
}
</style>
