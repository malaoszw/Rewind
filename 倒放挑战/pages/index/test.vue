<template>
	<view>
		<view class="box" style="">
			<view class="content title">音乐播放</view>
			<view class="cuIcon-videofill icon"></view>
		</view>
		<view class="" style="margin-top: 5%;">
			<view class="page-section page-section-gap" style="text-align: center;">
			</view>
		</view>
		<view  class="button_blue">
			<view class="cu-btn cuIcon bg-blue" :class="isPlay?'text-xxl':'text-xl'"	         
			@tap="clickPlay">
			<text :class="isPlay?'cuIcon-stop':'cuIcon-playfill'"></text>
			</view>
		</view>
		<view class="button_blue"><view class="cu-btn bg-blue round" @tap="clickPause">暂停</view>
		</view>
	</view>
</template>

<script>
const innerAudioContext = uni.createInnerAudioContext();
export default {
	data() {
		return {
			videoUrl:'https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.mp3',
			isPlay:false
		};
	},
	onLoad() {},
	mounted() {},
	methods: {
		clickPlay() {
			this.isPlay=true;
			innerAudioContext.src =this.videoUrl;
			innerAudioContext.play();
			innerAudioContext.onPlay(() => {
				console.log('开始播放');
			});
			innerAudioContext.onError(res => {
				console.log(res.errMsg);
				console.log(res.errCode);
			});
		},
		clickPause(){
			this.isPlay=false;
			innerAudioContext.pause();
			innerAudioContext.onPause(()=>{
				console.log("暂停")
			});
		},
	}
};
</script>

<style>
.box {
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
	margin-top: 10%;
}
.title {
	font-size: 50upx;
}
.icon {
	font-size: 50upx;
}
.button_blue {
	display: flex;
	justify-content: center;
	align-items: center;
	margin-top: 5%;
}
</style>
