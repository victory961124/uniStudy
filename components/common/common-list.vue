<template>
	<!-- 列表样式 -->
	<view class="p-2">
		<!-- 头像昵称|关注按钮 -->
		<view class="flex align-center justify-between">
			<view class="flex align-center">
				<!--头像-->
				<image :src="item.userpic" 
				class="mr-2 rounded-circle" 
				style="width: 65rpx;height: 65rpx;"
				@click="openspace"></image>
				
				<view>
					<view class="font" style="line-height: 1.5;">{{item.username}}</view>
					<text class="font-sm text-light-muted" style="line-height: 1.5;">{{item.newstime}}</text>
				</view>
			</view>
			<!-- 按钮 -->
			<view 
			class="flex align-center justify-center rounded bg-main text-white animated faster" 
			style="width: 90rpx;height: 50rpx;"
			hover-class="jello" 
			@click="follow"
			v-if="!item.isFollow"
			>
				关注
			</view>
		</view>
		<!-- 标题 -->
		<view class="font-md my-1" @click="openDetail">
			{{item.title}}
		</view>
		<!-- 图片 尽可能给具体的高度-->
		<image v-if="item.titlepic" :src="item.titlepic" 
		class="rounded w-100" style="height: 350rpx;"
		></image>
		<!-- 图标按钮 -->
		<view class="flex align-center">
			<!-- 顶 -->
			<view class="flex align-center justify-center flex-1 animated faster"  
			hover-class="jello text-main" @click="doSupport('support')"
			:class="item.support.type==='support'?'support-active':''">
				<text class="iconfont icon-dianzan2 mr-2"></text>
				<text>{{item.support.support_count===0?'顶':item.support.support_count}}</text>
			</view>
			<!-- 踩 -->
			<view class="flex align-center justify-center flex-1 animated faster" 
			hover-class="jello text-main"  @click="doSupport('unsupport')"
			:class="item.support.type==='unsupport'?'support-active':''">
				<text class="iconfont icon-cai  mr-2"></text>
				<text>{{item.support.unsupport_count===0?'踩':item.support.unsupport_count}}</text>
			</view>
			<!-- 评论 -->
			<view class="flex align-center justify-center flex-1 animated faster" 
			hover-class="jello text-main" @click="openDetail">
				<text class="iconfont icon-pinglun2 mr-2"></text>
				<text>{{item.comment_count>0?item.comment_count:'评论'}}</text>
			</view>
			<!-- 转发 -->
			<view class="flex align-center justify-center flex-1 animated faster" 
			hover-class="jello text-main" @click="openDetail">
				<text class="iconfont icon-fenxiang mr-2"></text>
				<text>{{item.share_num>0?item.share_num:'转发'}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			item:Object,
			index:Number,
		},
		methods:{
			//打开个人空间
			openspace(){
				console.log('打开个人空间');
			},
			//关注
			follow(){
				this.$emit("follow",this.index);
				// console.log('关注');
			},
			//进入详情页
			openDetail(){
				console.log('进入详情页');
			},
			//顶/踩操作
			doSupport(type){
				//通知父组件
				this.$emit('doSupport',{
					type:type,
					index:this.index
				})
			}
		}
	}
</script>

<style>
	.support-active{
		color: #FF4A6A;
	}
</style>
