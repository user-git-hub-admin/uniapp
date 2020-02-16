<template>
	<view>
		<view class="comms"><image src="../../static/images/back.png" @click="gos()"></image><text>{{clength}} 条评论</text></view>
		<view class="comment">
			<view class="sum">{{clength}}条评论</view>
			<dl class="commDl" v-for="com in comments">
				<dt><image :src="com.avatar"></image></dt>
				<dd class="first">{{com.author}}<image src="../../static/images/gengduo.png" class="more" @click="mores()"></image></dd>
				<dd>{{com.content}}</dd>
				<dd class="time"><text class="times">今天 19:00</text><text class="all">{{com.likes}}</text><image src="../../static/images/likes.png" class="one" @click="praise()"></image><image src="../../static/images/comments.png" class="two" @click="replay()"></image></dd>
			</dl>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				comments : [],
				clength : 0
			}
		},
		onLoad:function(){
			this.getComments()
		},
		methods: {
			gos(){
				uni.redirectTo({
					url: 'Details'
				});
			},
			mores(){
				console.log(111)
			},
			getComments(){
				var _thas = this;
				uni.request({
					url: 'http://news-at.zhihu.com/api/4/story/4232852/short-comments',
					method: 'GET',
					data: {},
					success: res => {
						console.log(res.data.comments);
						_thas.clength = res.data.comments.length
						for (var i=0 ; i<_thas.clength ; i++ ) {
							_thas.comments.push(res.data.comments[i])
						}
						_thas.getCommentss();
					},
					fail: () => {},
					complete: () => {}
				});
			},
			getCommentss(){
				var _thas = this;
				uni.request({
					url: 'http://news-at.zhihu.com/api/4/story/4232852/long-comments',
					method: 'GET',
					data: {},
					success: res => {
						console.log(res.data.comments);
						var leng = res.data.comments.length
						for (var i=0 ; i<leng ; i++ ) {
							_thas.comments.push(res.data.comments[i])
						}
						_thas.clength = _thas.clength+leng;
					},
					fail: () => {},
					complete: () => {}
				});
			},
			praise(){
				console.log(111);
			},
			replay(){
				uni.redirectTo({
					url: 'Replay'
				});
			},
		},
		
	}
</script>

<style>
.comms{text-align: center;position: relative;overflow: hidden;padding: 10px;}
.comms image{width: 25px;height: 25px;vertical-align: middle;position: absolute;left: 0;top: 7px;}
.comment,.comms{border-bottom: 1px solid #E5E5E5;}
.comms,.sum,.commDl .first{font-weight: bold;}
.commDl,.sum{padding: 10px 20px;}
.commDl dt image{width: 35px;height: 35px;border-radius: 50px;}
.commDl dt{float: left;}
.commDl dd{padding-left: 10px;overflow: hidden;line-height: 30px;font-size: 14px;}
.commDl dd image{width: 20px;height: 20px;vertical-align: middle;}
.commDl .first{position: relative;}
.commDl .first .more{position: absolute;right: 0px;top: 0;}
.commDl .times{padding-left: 30px;}
.commDl .time{position: relative;width: 100%;color: #ccc;}
.commDl .time .one{position: absolute;bottom: px;right: 80px;}
.commDl .time .two{float: right;padding-right: 20px;}
.commDl .time .all{position: absolute;right: 102px;top: -2px;}
</style>
