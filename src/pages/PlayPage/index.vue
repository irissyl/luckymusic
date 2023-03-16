<template>
	<view class="myaudio">
		<!-- 歌曲海报 -->
		<view class="musicimage" @click="changetomusic">
			<image class="appLogo"
				src="../../static/img/1.jpg"
				mode=""></image>
		</view>
		<!--  歌曲名称-->
		<view class="musictext" @click="changetomusic">
			{{text}}
		</view>
		<!-- 播放按钮 -->
		<view class="musiconplay">
			<view class="iconfont icon-bofanganniu" v-if=" iconshow ? false:true" @click="changeto">
 
			</view>
			<view class="iconfont icon-zanting" v-if=" iconshow ? true:false" @click="changeto">
 
			</view>
		</view>
		<!-- 列表按钮 -->
		<view class="musiclist">
			<view class="iconfont icon-bofangliebiao">
				<!-- v-if=" iconshow ? true:false" @click="changeto" -->
			</view>
		</view>
	</view>
</template>
 
<script>
	const innerAudioContext = uni.createInnerAudioContext() //想要实现暂停功能就要把该对象变为全局属性
	export default {
		name: 'myaudio',
		data() {
			return {
				iconshow: false,
				text: '红玫瑰 - 陈奕迅',
				url: "../../static/mp3/1.mp3",
				currenttime: 0
			}
		},
		methods: {
			changeto() {
				this.iconshow = !this.iconshow
				console.log(this.iconshow);
				if (this.iconshow) {
					innerAudioContext.src = this.url;
					innerAudioContext.seek(this.currenttime)
					innerAudioContext.volume = 0.5
					innerAudioContext.play()
					
				} else {
					innerAudioContext.pause()
					this.currenttime = innerAudioContext.currentTime
				}
 
 
			},
			changetomusic() {
				uni.navigateTo({
					url: "/pages/bofang/bofang"
				})
			},
 
		}
	}
</script>
 
<style lang="scss">
	@import url("../../static/iconfont/iconfont.css");
 
	// https://img2.baidu.com/it/u=3181851593,3353679262&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=292
	.myaudio {
		display: flex;
		flex-wrap: wrap;
		width: 100%;
		height: 100%;
		padding: 0;
		margin: 0;
 
		.musicimage {
			width: 15%;
			padding: 0;
			margin: 0;
			height: 100%;
			// background-color: black;
			border-radius: 50%;
 
			.appLogo {
				position: relative;
				top: 7px;
				left: 7px;
				width: 70%;
				height: 70%;
 
				border-radius: 50%;
			}
		}
 
		.musictext {
			width: 55%;
			height: 100%;
			padding-left: 10px;
			font-size: 15px;
			line-height: 50px;
			text-align: left;
		}
 
		@keyframes App-logo-spin {
			from {
				transform: rotate(0deg);
			}
 
			to {
				transform: rotate(360deg);
			}
		}
 
		@media (prefers-reduced-motion: no-preference) {
			.appLogo {
				animation: App-logo-spin infinite 20s linear;
			}
		}
 
		.musiconplay {
			width: 15%;
			height: 100%;
 
			.icon-bofanganniu {
				cursor: pointer;
				font-size: 30px;
				line-height: 50px;
			}
 
			.icon-zanting {
				font-size: 30px;
				line-height: 50px;
			}
		}
 
		.musiconplay:focus-visible {
			width: 15%;
			height: 100%;
			background-color: red;
 
			.icon-bofanganniu {
				font-size: 30px;
				line-height: 50px;
			}
 
			.icon-zanting {
				font-size: 30px;
				line-height: 50px;
			}
		}
 
		.musiclist {
			width: 12.1%;
			height: 100%;
 
			.icon-bofangliebiao {
				font-size: 30px;
				line-height: 50px;
				text-align: right;
			}
		}
	}
</style>