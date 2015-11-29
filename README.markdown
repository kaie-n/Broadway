A way to play back a background video animation on iPhone's Safari
===========
This is a fork of the [Broadway H.264 decoder](https://github.com/mbebenita/Broadway).
The focus here is on using that amazing decoder to play back H.264 encoded mp4 files as a gif replacment, where the HTML5 video tag is not suitable (Like in Safari on the iPhone, which doesn't allow inline videos as well as autoplay).

This solution is ready to be used on a website.
Check out the demo.html in the Player folder.

Limitations
===========
The entire video file has to be downloaded first by the client before it can be played back. If this is an issue for you, this fork isn't for you. You could build your own player with WebSockets based on [BroadwayStream](https://github.com/soliton4/BroadwayStream).

Only h.264 encoded mp4 files are supported. There are certain limitations on the encoding profile, weighted prediction for P-frames as well as CABAC entropy encoding are not supported by the Broadway decoder.

If you encode your videos with ffmpeg, here is an example:

    ffmpeg -y -i input.mp4 -vcodec libx264 -pass 1 -coder 0 -bf 0 -wpredp 0 -an -x264opts no-cabac:no-weightb -pix_fmt yuv420p -vf scale=568:320 output.mp4

Usage
===========
Load all of the .js files from the Player folder and add the following markup:

    <div class="broadway" src="video.mp4" loop="true" webgl="auto" workers="false" />

 Once the video is loaded, a canvas element is added to the div and the video frames are rendered to that canvas. Make sure your video is encoded regarding the above mentioned limitations.