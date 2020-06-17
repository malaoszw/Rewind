<template>
	<view >
		<view class="box" style="">
			<view class="content title">倒放挑战</view>
			<view class="cuIcon-videofill icon"></view>
		</view>
		<view class="" style="margin-top: 5%;">
			<view class="page-section page-section-gap" style="text-align: center;">
			 </view>
		</view>
		<view v-if="!isPlay" class="button_blue">
			<view class="cu-btn bg-blue round" @tap="clickPlay">
				播放
			</view>
		</view>
		<view v-else class="button_blue">
			<view class="cu-btn bg-blue round" @click="clickPlay">
				暂停
			</view>
		</view>
	 	<view  class="button_blue">  
            <button @tap="startRecord">开始录音</button>
            <button @tap="endRecord">停止录音</button>
            <button @tap="playVoice">播放录音</button>
		</view>
	</view>
</template>

<script>
	const recorderManager = uni.getRecorderManager();
	const innerAudioContext = uni.createInnerAudioContext();
	
	//const innerAudioContext=uni.createInnerAudioContext();
	//innerAudioContext.loop=true;
	//innerAudioContext.src = 'https://sy-sycdn.kuwo.cn/a61ec25d60aaa643065067ee55727cb0/5ebe8751/resource/n2/99/30/814703912.mp3';
export default {
	data() {
		return {
			video:[
				'https://sy-sycdn.kuwo.cn/a954366e7e4af5b10a4a41f9896e2613/5ebee162/resource/n2/99/30/814703912.mp3',
				'https://ip-h5-nf01-sycdn.kuwo.cn/2695b8c2f3e3585fe6d1df3a60a82c3e/5ebf940a/resource/n1/16/65/2891437997.mp3',
			    'https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.mp3',
			],
			isPlay:false,
			voicePath: ''
		};
	},
	onLoad() {
		let self = this;
		recorderManager.onStop(function (res) {
		    console.log('recorder stop' + JSON.stringify(res));
		    self.voicePath = res.tempFilePath;
		});
		uni.setInnerAudioOption({
			mixWithOther: true,
			obeyMuteSwitch: false,
		});
	},
	mounted() {
	},
	methods: {
		clickPlay(){
			/*var videoUrl='https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.mp3';*/
			/*innerAudioContext.loop=true;
			innerAudioContext.src = videoUrl;*/
			this.isPlay=!this.isPlay;
			this.Audio(this.video[1]);
		},
		Audio(e){
			//console.log('首次播放'+innerAudioContext.paused);
			if(this.isPlay)
			{
				innerAudioContext.src = e;
				innerAudioContext.play();
				innerAudioContext.onPlay(() => {
					console.log('首次播放'+innerAudioContext.paused);
					
				});
			}else{
				innerAudioContext.pause();
				innerAudioContext.onPause(()=>{
					console.log('暂停'+innerAudioContext.paused);
					
				});
			}
			

			    //console.log('首次播放'+innerAudioContext.paused);
			
	
		},
		clickPause(){	
			/*this.isPlay=!this.isPlay;
			this.Audio(this.video[1]);*/
			/*this.isPlay=!this.isPlay;
			this.Audio(this.video[0]);*/
		},
		playAudio(){},
		   startRecord() {
            console.log('开始录音');

            recorderManager.start();
        },
        endRecord() {
            console.log('录音结束');
            recorderManager.stop();
        },
        playVoice() {
            console.log('播放录音');
			//innerAudioContext.obeyMuteSwitch=false;
			innerAudioContext.autoplay = true;
            if (this.voicePath) {
                innerAudioContext.src = this.voicePath;
                innerAudioContext.play();
            }
        }
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
.button_blue{
	display: flex;
	justify-content: center;
	align-items: center;
	margin-top: 5%;
}
</style>
