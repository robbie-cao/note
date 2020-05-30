# youtube-dl

- http://ytdl-org.github.io/youtube-dl/
- https://askubuntu.com/questions/486297/how-to-select-video-quality-from-youtube-dl
- https://askubuntu.com/questions/210410/how-to-run-youtube-dl-through-proxy-server
- https://unix.stackexchange.com/questions/71481/how-to-use-socks-proxy-for-commands-in-terminal-such-as-youtube-dl

```
$ youtube-dl "youtube.com/watch?v=3XjwiV-6_CA"
$ export http_proxy=http://localhost:8035/ https_proxy=http://localhost:8035/
$ youtube-dl youtube.com/watch?V=3XjwiV-6_CA
```


youtube-dl works well with proxychains on ubuntu. Make sure ur tunneling via command line.

```
$ ssh -D 8081 ubuntu@yourSSHserver
```

next install proxychains on your localhost not the ssh server ur conncted to.

```
$ sudo apt-get install proxychains
```

edit your proxychains config file

```
$ sudo nano /etc/proxychains.conf
```

edit the port number on the last line

```
socks4  127.0.0.1 8081
```

Note:I'm using proxychains on port 8081

then just add proxychains to the begining of the command when using youtube-dl

```
$ proxychains ./youtube-dl http://thesite.com/yourvideo.hmtl 
```

Since `youtube-dl` version `2016.05.10`, you can use `--proxy to specify` SOCKS proxy, e.g.

```
$ youtube-dl --proxy "socks5://127.0.0.1/" -v 9bZkp7q19f0
```

`--proxy` URL Use the specified HTTP/HTTPS/SOCKS proxy.

To enable experimental SOCKS proxy, specify a proper scheme. For example `socks5://127.0.0.1:1080/`.



Have it grab the best single file which contains both video and audio in one instead, with this:

```
$ youtube-dl -f best https://youtu.be/FWGC9SqA3J0
```

More specifically, see below for the results of running

```
$ youtube-dl -F https://youtu.be/FWGC9SqA3J0
```

in order to see what video 'F'ormats are availabe for download:

```
gabriel ~ $ youtube-dl -F https://youtu.be/FWGC9SqA3J0
[youtube] FWGC9SqA3J0: Downloading webpage
[youtube] FWGC9SqA3J0: Downloading video info webpage
[youtube] FWGC9SqA3J0: Downloading MPD manifest
[youtube] FWGC9SqA3J0: Downloading MPD manifest
[info] Available formats for FWGC9SqA3J0:
format code  extension  resolution note
139          m4a        audio only DASH audio   50k , m4a_dash container, mp4a.40.5@ 48k (22050Hz), 2.30MiB
249          webm       audio only DASH audio   51k , opus @ 50k, 2.34MiB
250          webm       audio only DASH audio   62k , opus @ 70k, 2.85MiB
171          webm       audio only DASH audio  103k , vorbis@128k, 4.68MiB
251          webm       audio only DASH audio  109k , opus @160k, 5.10MiB
140          m4a        audio only DASH audio  130k , m4a_dash container, mp4a.40.2@128k (44100Hz), 6.13MiB
160          mp4        256x138    DASH video  108k , mp4_dash container, avc1.4d400b, 24fps, video only
134          mp4        640x348    DASH video  142k , mp4_dash container, avc1.4d401e, 24fps, video only, 3.42MiB
133          mp4        426x232    DASH video  242k , mp4_dash container, avc1.4d400c, 24fps, video only
136          mp4        1280x694   DASH video  473k , mp4_dash container, avc1.4d401f, 24fps, video only, 8.01MiB
135          mp4        854x464    DASH video 1155k , mp4_dash container, avc1.4d4014, 24fps, video only
17           3gp        176x144    small , mp4v.20.3, mp4a.40.2@ 24k, 1.63MiB
36           3gp        320x174    small , mp4v.20.3, mp4a.40.2, 2.98MiB
43           webm       640x360    medium , vp8.0, vorbis@128k, 7.44MiB
18           mp4        640x348    medium , avc1.42001E, mp4a.40.2@ 96k, 8.54MiB
22           mp4        1280x694   hd720 , avc1.64001F, mp4a.40.2@192k (best) 
```

Notice that row 22 says "(best)" to the far right of it. This is the only option which offers hd720 quality, which is the best quality I can get when watching this video in a web browser on YouTube. It is the clearest and has the best definition. When I use either of the commands recommended by the top answer:

```
$ youtube-dl -f bestvideo+bestaudio https://youtu.be/FWGC9SqA3J0
```

OR:

```
$ youtube-dl -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/bestvideo+bestaudio' --merge-output-format mp4 https://youtu.be/FWGC9SqA3J0

```
