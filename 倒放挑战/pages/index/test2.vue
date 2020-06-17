<template>
	<view>
		<audio :src="src" id="myAudio"></audio>
		<button type="primary" bindtap="audioPlay">播放</button>
		<button type="primary" bindtap="audioPause">暂停</button>
		<button type="primary" bindtap="audio14">设置当前播放时间为14秒</button>
		<button type="primary" bindtap="audioStart">回到开头</button>
	</view>
</template>

<script>
export default {
	onReady(e) {
		// 使用 wx.createAudioContext 获取 audio 上下文 context
		this.audioCtx = uni.createAudioContext('myAudio');
		this.audioCtx.setSrc(
			'https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.mp3'
		);
		this.audioCtx.play();
	},
	data() {
		return {
			src:''
		};
	},
	audioPlay() {
		this.audioCtx.play();
	},
	audioPause() {
		this.audioCtx.pause();
	},
	audio14() {
		this.audioCtx.seek(14);
	},
	audioStart() {
		this.audioCtx.seek(0);
	}
};
</script>

<style></style>
