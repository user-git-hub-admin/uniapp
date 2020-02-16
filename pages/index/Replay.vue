<template>
	<view>
		<view class="replay"><image src="../../static/images/back.png" @click="replays()"></image>回复谁<text class="blue" @click="issue()">发布</text></view>
		<view class="lun">友善的评论是交流的起点</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods:{
			replays(){
				uni.redirectTo({
					url: 'Comment'
				});
			},
			issue(){
				console.log(2)
			}
		},
	}
</script>

<style>
.replay{padding: 10px;text-align: center;position: relative;border-bottom: 1px solid #E5E5E5;}
.replay image{width: 25px;height: 25px;vertical-align: middle;position: absolute;left: 5px;top: 10px;}
.replay .blue{color: #007AFF;position: absolute;right: 10px;top: 10px;}
.lun{padding: 20px 10px;color: #CCC;font-size: 14px;}
</style>