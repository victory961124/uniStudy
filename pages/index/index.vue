<template>
	<view>
		<!-- 顶部选项卡-->
		<scroll-view scroll-x :scroll-into-view="tabInto" 
		scroll-with-animation style="height: 100rpx;" 
		class="scroll-row border-bottom border-light-secondary">
			<view class="scroll-row-item px-3 py-2 font-md" 
			v-for="(item,index) in tabBars" :key="index" :id="item.id"
			:class="tabIndex===index?'text-main font-lg font-weight-bold':''"
			 @click="changeTab(index)">
				{{item.name}}
			</view>
		</scroll-view>

		<swiper :duration="150" :current="tabIndex" @change="onChangeTab" 
		:style="'height:'+scrollH+'px;'">
			<swiper-item v-for="(item,index) in newsList" :key="index">
				<scroll-view scroll-y="true" :style="'height:'+scrollH+'px;'">
					<block v-for="(item2,index2) in item.list" :key="index2">
						<!-- 列表组件 -->
						<common-list :item="item2" :index="index2" @follow="follow" @doSupport="doSupport"></common-list>
						<!-- 全局分割线 -->
						<divider></divider>
					</block>
				</scroll-view>
			</swiper-item>
		</swiper>

	</view>
</template>

<script>
	import commonList from '@/components/common/common-list.vue'
	export default {
		components: {
			commonList
		},
		data() {
			return {
				scrollH: 600,
				tabInto: "",
				tabIndex: 0,
				// 顶部选项卡
				tabBars: [{
					name: '关注',
					id: 'tab0',
				}, {
					name: '推荐',
					id: 'tab1',
				}, {
					name: '体育',
					id: 'tab2',
				}, {
					name: '热点',
					id: 'tab3',
				}, {
					name: '热点1',
					id: 'tab4',
				}, {
					name: '热点2',
					id: 'tab5',
				}, {
					name: '热点3',
					id: 'tab6',
				}, {
					name: '热点4',
					id: 'tab7',
				}, ],
				newsList: []
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: res => {
					console.log(res);
					this.scrollH = res.windowHeight - uni.upx2px(101)
					console.log(this.scrollH)
				}
			})
			this.getData();
		},
		methods: {
			getData() {
				var arr = []
				for (let i = 0; i < this.tabBars.length; i++) {
					let obj = {
						list: [{
								username: "昵称",
								userpic: "../../static/default.jpg",
								newstime: "2019-10-20 下午04:30",
								isFollow: false,
								title: "我是标题",
								titlepic: "../../static/demo/datapic/11.jpg",
								support: {
									type: "support",
									support_count: 1,
									unsupport_count: 2
								},
								comment_count: 3,
								share_num: 4,
							},
							{
								username: "昵称",
								userpic: "../../static/default.jpg",
								newstime: "2019-10-20 下午04:30",
								isFollow: false,
								title: "我是标题",
								titlepic: "",
								support: {
									type: "unsupport",
									support_count: 1,
									unsupport_count: 2
								},
								comment_count: 1,
								share_num: 2,
							},
							{
								username: "昵称",
								userpic: "../../static/default.jpg",
								newstime: "2019-10-20 下午04:30",
								isFollow: false,
								title: "我是标题",
								titlepic: "",
								support: {
									type: "",
									support_count: 0,
									unsupport_count: 0
								},
								comment_count: 0,
								share_num: 0,
							}
						]
					}
					arr.push(obj)
				}
				this.newsList = arr
			},
			onChangeTab(e) {
				this.changeTab(e.detail.current)
			},
			//切换选项
			changeTab(index) {
				if (this.tabIndex !== index) {
					this.tabIndex = index;
					this.tabInto = "tab" + index;
					console.log('已切换')
				}

			},
			follow(e) {
				this.list[e].isFollow = true;
				uni.showToast({
					title: "关注成功!"
				})
			},
			//顶踩操作
			doSupport(e) {
				let item = this.list[e.index];
				let msg = e.type === 'support' ? '顶' : '踩';
				if (item.support.type === '') {
					item.support[e.type + '_count']++;
				}
				if (item.support.type === 'support' && e.type === 'unsupport') {
					item.support.support_count--;
					item.support.unsupport_count++;
				} else if (item.support.type === 'unsupport' && e.type === 'support') {
					item.support.support_count++;
					item.support.unsupport_count--;
				}
				item.support.type = e.type;
				uni.showToast({
					title: msg + '成功!'
				})
			}
		}
	}
</script>

<style>

</style>
