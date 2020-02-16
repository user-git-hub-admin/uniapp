<template>
	<view>
		<view v-html="details"></view>
		<view class="comment">
			<view class="comOne" @click="back()"><image src="../../static/images/back.png"></image></view>
			<view @click="pingLun()"><image src="../../static/images/comment.png"></image><text>5</text></view>
			<view @click="zan()"><image v-bind:src="fabulou > 0 ? '../../static/images/like2.png' : '../../static/images/like.png' "></image></image><text>{{fabulous}}</text></view>
			<view @click="cang()"><image v-bind:src="pic > 0 ? '../../static/images/collect2.png' : '../../static/images/collect.png' "></image></view>
			<view class="button" type="primary" @click="togglePopup('bottom', 'share')"><image src="../../static/images/transmit.png"></image><text>5</text></view>
		</view>
		<!-- 底部分享弹窗 -->
		<uni-popup ref="showshare" :type="type" @change="change">
			<view class="uni-share">
				<text class="uni-share-title">分享到</text>
				<view class="uni-share-content">
					<view v-for="(item, index) in bottomData" :key="index" class="uni-share-content-box">
						<view class="uni-share-content-image">
							<image :src="item.icon" class="content-image" mode="widthFix" />
						</view>
						<text class="uni-share-content-text">{{ item.text }}</text>
					</view>
				</view>
				<text class="uni-share-btn" @click="cancel('share')">取消分享</text>
			</view>
		</uni-popup>
	</view>
</template>

<script>	
	import uniSection from '@/components/uni-section/uni-section.vue'
	import uniPopup from '@/components/uni-popup/uni-popup.vue'
	import uniIcons from '@/components/uni-icons/uni-icons.vue'
	var csses;
	export default {
		components: {
			uniSection,
			uniPopup,
			uniIcons
		},
		data(){
			return{
				details : '',
				fabulous : 0,
				fabulou : 0,
				pic :0,
				bottomData: [{
						text: '微信',
						icon: 'https://img-cdn-qiniu.dcloud.net.cn/uni-ui/grid-2.png',
						name: 'wx'
					},
					{
						text: '支付宝',
						icon: 'https://img-cdn-qiniu.dcloud.net.cn/uni-ui/grid-8.png',
						name: 'wx'
					},
					{
						text: 'QQ',
						icon: 'https://img-cdn-qiniu.dcloud.net.cn/uni-ui/gird-3.png',
						name: 'qq'
					},
					{
						text: '新浪',
						icon: 'https://img-cdn-qiniu.dcloud.net.cn/uni-ui/grid-1.png',
						name: 'sina'
					},
					{
						text: '百度',
						icon: 'https://img-cdn-qiniu.dcloud.net.cn/uni-ui/grid-7.png',
						name: 'copy'
					},
					{
						text: '其他',
						icon: 'https://img-cdn-qiniu.dcloud.net.cn/uni-ui/grid-5.png',
						name: 'more'
					}
				],
			}
		},
		onLoad:function(){
			this.getDetails()
		},
		methods:{
			getDetails(){
				var _thas = this;
				uni.request({
					url: 'http://news-at.zhihu.com/api/4/news/3892357',
					method: 'GET',
					data: {},
					success: res => {
						console.log(res.data.css);
						_thas.details=res.data.body;
						csses=res.data.css;
						console.log(csses);
					},
					fail: () => {},
					complete: () => {}
				});
			},
			back(){
				uni.redirectTo({
					url: 'index'
				});
			},
			pingLun(){
				uni.redirectTo({
					url: 'Comment'
				});
			},
			zan(){
				// this.fabulous = this.fabulous+1;
				if(this.fabulou == 1){
					this.fabulous = this.fabulous-1;
					this.fabulou = 0;
				}else{
					this.fabulous = this.fabulous+1;
					this.fabulou = 1;
				}
				console.log(this.fabulou);
			},
			cang(){
				if(this.pic == 1){
					this.pic=0
				}else{
					this.pic=1
				}
				console.log(this.pic);
			},
			togglePopup(type, open) {
				switch (type) {
					case 'top':
						this.content = '顶部弹出 popup'
						break

					case 'bottom':
						this.content = '底部弹出 popup'
						break
					case 'center':
						this.content = '居中弹出 popup'
						break
				}
				this.type = type
				this.$nextTick(() => {
					this.$refs['show' + open].open()
				})
			},
			change(e) {
				console.log('是否打开:' + e.show)
			},
			cancel(type) {
				this.$refs['show' + type].close()
			},
		}
	}
	
</script>

<style>
/* 	@import url("http://news-at.zhihu.com/css/news_qa.auto.css?v=4b3e3"); */
.comment image{width: 30px;height: 30px;vertical-align: middle;}
.comment view{float: left;width: 19%;text-align: center;margin:30upx 0 10upx 0;position: relative;}
.comment .comOne{border-right: 1px solid #999;}
.comment view text{position: absolute;right: 4px;top: 0;font-size: 14px;}

/* 底部分享 */
	.uni-share {
		/* #ifndef APP-NVUE */
		display: flex;
		flex-direction: column;
		/* #endif */
		background-color: #fff;
	}

	.uni-share-title {
		line-height: 60rpx;
		font-size: 24rpx;
		padding: 15rpx 0;
		text-align: center;
	}

	.uni-share-content {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
		padding: 15px;
	}

	.uni-share-content-box {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
		width: 200rpx;
	}

	.uni-share-content-image {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		justify-content: center;
		align-items: center;
		width: 60rpx;
		height: 60rpx;
		overflow: hidden;
		border-radius: 10rpx;
	}

	.content-image {
		width: 60rpx;
		height: 60rpx;
	}

	.uni-share-content-text {
		font-size: 26rpx;
		color: #333;
		padding-top: 5px;
		padding-bottom: 10px;
	}

	.uni-share-btn {
		height: 90rpx;
		line-height: 90rpx;
		font-size: 14px;
		border-top-color: #f5f5f5;
		border-top-width: 1px;
		border-top-style: solid;
		text-align: center;
		color: #666;
	}
</style>