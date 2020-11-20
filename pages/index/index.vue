<template>
	<view>
		<block v-for="(item,index) in list" :key="index">
		<!-- 列表组件 -->
		<common-list :item="item" :index="index"></common-list>
		<!-- 全局分割线 -->
		<divider></divider>
		</block>
	</view>
</template>

<script>
	import commonList from '@/components/common/common-list.vue'
	export default {
		components:{commonList},
		data() {
			return {
				list:[{
					username:"昵称",
					userpic:"../../static/default.jpg",
					newstime:"2019-10-20 下午04:30",
					isFollow:false,
					title:"我是标题",
					titlepic:"../../static/demo/datapic/11.jpg",
					support:{
						type:"support",
						support_count:1,
						unsupport_count:2
					},
					comment_count:3,
					share_num:4,
				},{
					username:"昵称",
					userpic:"../../static/default.jpg",
					newstime:"2019-10-20 下午04:30",
					isFollow:false,
					title:"我是标题",
					titlepic:"../../static/demo/datapic/11.jpg",
					support:{
						type:"support",
						support_count:1,
						unsupport_count:2
					},
					comment_count:3,
					share_num:4,
				}]
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	
</style>
