<template>
	<view class="mine">
		<view class="return" @click="returns()"><image src="../../static/images/back.png"></image></view>
		<view class="headPportrait">
			<image src="../../static/images/tuoyuan.png"></image>
			<text>Monsters</text>
		</view>
		<view class="collect" @click="rate()">我的收藏<image src="../../static/images/moress.png"></image></view>
		<view class="collect" @click="rate()">消息中心<image src="../../static/images/moress.png"></image></view>
		<view class="pattern">
			<view class="patLeft"  @click="night()"><image src="../../static/images/night.png"></iamge><text>夜间模式</text></view>
			<view class="patRight"><image src="../../static/images/night.png"></iamge><text @click="set()">设置</text></view>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				
			}
		},
		methods:{
			night(){
				console.log(111);
			},
			returns(){
				uni.redirectTo({
					url: 'index'
				});
			}
		}
	}
</script>

<style>
.return image{width: 25px;height: 25px;padding:20upx 0 0 20upx}
.headPportrait{text-align: center;padding: 20upx 0;}
.headPportrait image{width: 105upx;height: 105upx;vertical-align: middle;}
.headPportrait text{display: block;font-weight: bold;}
.collect{border-top: 1px solid #ccc;line-height: 80upx;padding-left: 50upx;}
.collect image{float: right;width: 30px;height: 30px;padding-right: 20upx;}
.pattern{overflow: hidden;margin-top: 400px;}
.pattern .patLeft{width: 50%;text-align: center;float: left;}
.patLeft image,.patRight image{width: 60upx;height: 60upx;display: block;margin: 0 auto;padding-bottom: 10upx;}
.pattern .patRight{width: 50%;text-align: center;float: left;}
</style>