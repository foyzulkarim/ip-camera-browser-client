# video-streaming

## Stream IP Camera to VLC player
- For the case of `TP-Link C200` model the URL I used = rtsp://{username}:{password}@{ip}:554/stream1
- Input the URL in Network Stream

![image](https://user-images.githubusercontent.com/497812/118369633-ac1ad300-b5d6-11eb-85a2-6367b4b929ca.png)


## Convert stream to HLS
Execute FFMPEG command

`.\server\libs\ffmpeg.exe -i rtsp://{username}:{password}@{ip}:554/stream1 -fflags flush_packets -max_delay 5 -flags -global_header -hls_time 5 -hls_list_size 3 -vcodec copy -y .\videos\ipcam\index.m3u8`

![image]()


## Install the packages 
- Open new terminal tab
- Go inside server folder
- Run `npm install`

## Cleanup streamed `.ts` files
- Open new terminal tab
- Go inside server folder
- Run `.\node_modules\.bin\nodemon .\cleaner.js`

## Serve the auto generated hls (m3u8) file
- Open new terminal tab
- Go inside server folder
- Run  `.\node_modules\.bin\nodemon .\hls-server.js`

## Test hls file in https://hls-js-dev.netlify.app/demo/ site
- Visit `https://hls-js-dev.netlify.app/demo`
- Input the m3u8 url and press `Apply` 
![image]()


## Run react client
- Open new terminal tab
- Go inside `client\hls-client` folder
- Run `npm install`
- Run `npm start`
![image]()