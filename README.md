# netease-f2e-video
netease f2e video

## 视频自适应全屏实现方法

### html
```
<div class="video-wrap">
		<video class="video" poster="poster.jpg" src="video.mp4" x-webkit-airplay="true" playsinline="true" webkit-playsinline="true" x5-video-player-type="h5" x5-video-player-fullscreen="true"></video>
		
	<!-- 安卓下显示 -->
	<div class="video-poster">
		<!-- 默认播放图标 可自行更换 -->
		<div class="play-icon"></div>
	</div>
</div>
```

### css
```
.video-wrap {
	width: 100%;
	height: 100%;
	position: absolute;
	top: 0;
	left: 0;
}
.video{
	width:100%;
	height:100%;
	object-fit: fill;
}
.video-poster {
	width: 100%;
	height: 100%;
	background: url(poster.jpg) no-repeat center center;
	background-size: 100% 100%;
	display: none;
}
.video-poster .play-icon {
	width: 2rem;
	height: 2rem;
	background: url(play-icon.png) no-repeat center center;
	background-size: cover;
	position: absolute;
	left: 0;
	top: 0;
	right: 0;
	bottom: 0;
	margin: auto;
	pointer-events: none;
}

```


### js
```
	//提前加载下视频
	$('.video')[0].load();
	$(document).on('WeixinJSBridgeReady', function () {
	    $('.video')[0].load();
	});
	
	
	//安卓下
	if (netease.ua.android) {
		$('.video-poster').show();
		$('.video-poster').on('click', function () {
			$(this).hide();
			$('.video)[0].play();
			return false;
		});
	}
	//安卓下注意事项
	//video的object-fit值和video-poster的backdground-size值是对应的
	//object-fit: cover    backdground-size: cover
	//object-fit: contain  backdground-size: contain
	//object-fit: fill     backdground-size: 100% 100%
	
	
	//ios下
	//loading完后可以直接播放$('.video)[0].play();
	
	
	//loading结束后回调
	function loadEndedCallBack () {
		$('.video')[0].play();
	}
	
	
	
	
```
### demo

[demo](http://test.go.163.com/web/sale_go/20180329_f2e-video/index.html)
