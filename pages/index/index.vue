<template>
	<view class="index">
		<view class="indexHead">
			<view class="date" >{{day}}<text>{{month}}</text></view>	
			
			<view class="daily hours">{{hours}}</view>
			<view class="homePage" @click="tiao()"><image src="../../static/images/tuoyuan.png" ></image></view>
		</view>
		<view class="box">
			<!-- indexBanner驼峰式命名 -->
			<view class="indexBanner">
				<!-- autoplay interval  2秒轮播一次 1000=1秒
				indicator-dots 是否显示指示点
				indicator-color 默认状态下指示点的颜色
				indicator-active-color 图片轮播之后指示点现实的颜色
				 -->
				<swiper autoplay interval="2000" indicator-dots  indicator-color="#666"  indicator-active-color="#ccc">
					<swiper-item v-for="(item,index) in list" :key="index">
						<image :src="item.image"></image>
						<view>{{item.title}}</view>
					</swiper-item>
				</swiper>
			</view>
		</view>
		<!-- <view class="texts">刷快手和看莎士比亚有什么区别<text class="author">作者/大象公会</text></view> -->
		<view class="listDl">
			<dl v-for="(n,dls) in news" :key="dls" @click="bot()">
				<dt><image :src="n.images"></image></dt>
				<dd>{{n.title}}</dd>
				<dd class="read">{{n.hint}}</dd>
			</dl>
		</view >
	</view>
</template>

<script>
	export default {
		data() {
			return {
				day : '',
				month : '',	
				news : [],
				list:[],
		    articleList:[],
				hours : ''
			} //return
		},
		onLoad:function(){
			var _thes = this;
			this.getNews();
			this.day = new Date().getDate();
			this.getMonths();
			this.getHourses();
			console.log(_thes.hours);			
		},
		onPullDownRefresh:function(){			
			this.getNews();			
		},
		methods: {  
			getNews : function(){
				var _thas = this;
				console.log(111) ;
				uni.request({		
					url: 'http://news-at.zhihu.com/api/4/news/latest',
					method: 'GET',
					data: {},
					success: res => {
						 console.log(res.data);
						// var list=res.data.split('--hcSplitor');
						// _self.list=list;
						for(var i=0;i<res.data.stories.length;i++){
							_thas.news.push(res.data.stories[i])
						}
						for(var i=0;i<res.data.top_stories.length;i++){
							_thas.list.push(res.data.top_stories[i])
						}
						console.log(_thas.news);
						uni.stopPullDownRefresh();
					},
					fail: () => {},
					complete: () => {}
				});
			},
			tiao(){
				uni.redirectTo({
					url: 'Mine'
				});
			},
			bot(){
				uni.redirectTo({
					url: 'Details'
				});
			},
			getMonths(){
					var _thas = this;
					switch (new Date().getMonth()+1){
						case 1:
						_thas.month = '一月';
						break;
						case 2:
						_thas.month = '二月';
						break;
						case 3:
						_thas.month = '三月';
						break;
						case 4:
						_thas.month = '四月';
						break;
						case 5:
						_thas.month = '五月';
						break;
						case 6:
						_thas.month = '六月';
						break;
						case 7:
						_thas.month = '七月';
						break;
						case 8:
						_thas.month = '八月';
						break;
						case 9:
						_thas.month = '九月';
						break;
						case 10:
						_thas.month = '十月';
						break;
						case 11:
						_thas.month = '十一月';
						break;
						case 12:
						_thas.month = '十二月';
						break;
						default:
							_thas.month = '错误';
							break;
					}		
			},
			getHourses(){
				var _thas =  this;
				var h = new Date().getHours();
				
				if(0<=h&& h<6){
				 return  _thas.hours = '早晨好';
				}
				if(6<=h&& h<11){
				 return _thas.hours = '上午好';
				}
				if(11<=h&& h<13){
				 return _thas.hours = '中午好';
				}
				if(13<=h&& h<17){
				 return _thas.hours = '下午好';
				}
				if(17<=h&& h<24) {
				 return _thas.hours = '晚上好';
				}
		}
	}
	}
</script>

<style>
.indexHead{overflow: hidden;padding: 10px 0;}	
.indexHead .date,.indexHead .daily{float: left;}
.indexHead .date{font-weight: bold;border-right: 1px solid #D3D3D3;padding: 0 15px;}
.indexHead .date text{display: block;font-size: 12px;}
.indexHead .hours{font-weight: normal;}
.indexHead .daily{font-size: 28px;font-weight: bold;padding-left: 15px;}
.indexHead .homePage{float: right;padding: 5px 15px 0 0;}
.indexHead .homePage image{width: 35px;height:35px;}
.indexBanner image{width: 100%;height: 100%;}
.texts{position: absolute;left: 0;top: 150px;color: #fff;}
.texts .author{display: block;font-size: 14px;color: #999;padding-top: 5px;}
.listDl{padding: 15px;}
.listDl dl{overflow: hidden;padding: 10upx 0;}
.listDl dl dt image{width: 85px;height: 80px;border-radius: 5px;}
.listDl dl dt{float: right;}
.listDl dl dd{font-size: 16px;font-weight: bold;}
.listDl dl .read{font-size: 14px;color: #999;padding-top: 20upx;font-weight: normal;}
</style>
