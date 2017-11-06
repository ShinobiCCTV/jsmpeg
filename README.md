# JSMpeg – Play data like it's 2017

This version of JSMpeg is modified to allow dynamic writing to the player. This is useful for methods not written to be apart of the player like direct use of `socket.io`. 

```
JSMpeg is a Video Player written in JavaScript. It consists of an MPEG-TS demuxer, MPEG1 video & MP2 audio decoders, WebGL & Canvas2D renderers and WebAudio sound output. JSMpeg can load static videos via Ajax and allows low latency streaming (~50ms) via WebSockets.

JSMpeg can decode 720p Video at 30fps on an iPhone 5S, works in any modern browser (Chrome, Firefox, Safari, Edge) and comes in at just 20kb gzipped.

Some more info and demos: [jsmpeg.com](http://jsmpeg.com/)
```

## Usage (Modified for jsmpeg.pipe.js)

Basic usage of jsmpeg-pipe with a socket.io client. More details about using this file can be found here. https://gist.github.com/mehdi-elhaij/19c9955e1754810cdedeb9c325ae3e0b

```
<script src="/libs/js/socket.io.js"></script>
<script src="/libs/js/jsmpeg.pipe.js"></script>
<canvas id="canvas" height=500 width=500></canvas>
<script>
    var socket = io();
    console.log(socket)
    socket.on('connect',function(){
        //pretend this is the command you use to initiate getting H.264 (MPEG) data
        socket.emit('f',{function:'getStream',feed:'2'})
    })
    // initiate a player that can be piped to.
    var player = new JSMpeg.Player('pipe',{
        canvas:document.getElementById('canvas')
    });
    socket.on('h264', function (data) {
        // pretend you are getting data as follows
        // data = {buffer:ArrayBuffer}
        player.write(data.buffer)
    });
</script>
```

JSMpeg is made by Dominic Szablewski – http://phoboslab.org

http://jsmpeg.com 

```
# With JSMpeg you get:
- A video and audio format that works in all modern browsers.
- No licensing fees. All MPEG1 and MP2 patents have expired.
- Very tight control over the Audio and Video decoders to implement your ideas.
- Very low latency realtime streaming with high framerates and acceptable quality and bitrates.
- A stack that you can understand from top to bottom.
```