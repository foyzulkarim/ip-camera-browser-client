# How to stream your IP Camera into browser

## YouTube explanation and demo

[![YouTube explanation](https://img.youtube.com/vi/Acmng0FHHqI/0.jpg)](https://www.youtube.com/watch?v=Acmng0FHHqI)

# Steps

## Stream IP Camera to VLC player
- For the case of `TP-Link C200` model the URL I used = `rtsp://{username}:{password}@{ip}:554/stream1`
- Input the URL in Network Stream

![image](https://user-images.githubusercontent.com/497812/118369633-ac1ad300-b5d6-11eb-85a2-6367b4b929ca.png)


## Convert stream to HLS
Execute FFMPEG command

`.\server\libs\ffmpeg.exe -i rtsp://{username}:{password}@{ip}:554/stream1 -fflags flush_packets -max_delay 5 -flags -global_header -hls_time 5 -hls_list_size 3 -vcodec copy -y .\videos\ipcam\index.m3u8`

After successful execution, we should see the converted video files (`index.m3u8 *.ts`)

![image](https://user-images.githubusercontent.com/497812/118370441-4c262b80-b5da-11eb-97bb-4d5909f00b83.png)



## Install the packages 
- Open new terminal tab
- Go inside server folder
- Run `npm install`

## Cleanup streamed `.ts` files
- Open new terminal tab
- Go inside server folder
- Run `.\node_modules\.bin\nodemon .\cleaner.js`
- This will delete the streamed/served `.ts` files from local directory to save the space

## Serve the auto generated hls (m3u8) file
- Open new terminal tab
- Go inside server folder
- Run  `.\node_modules\.bin\nodemon .\hls-server.js`

## Test hls file in browser
- Visit [`cookpete.com/react-player`](https://cookpete.com/react-player).
- Input the m3u8 url [http://localhost:4000/index.m3u8] and press `Load` 
![image](https://user-images.githubusercontent.com/497812/118370576-d2427200-b5da-11eb-83b1-dd49a0c5de43.png)


## Run react client
- Open new terminal tab
- Go inside `client\hls-client` folder
- Run `npm install`
- Run `npm start`

![image](https://user-images.githubusercontent.com/497812/118370619-087ff180-b5db-11eb-94da-19ce190a87f6.png)


# Notes
It is possible to automate all of the commands under simplified `npm start` command in server project. However, for better understanding of how things work and better clarity, I break down the steps and showed how easy it is to actually stream your IP Camera to your browser. 

If you have real IP from your ISP, you can point your Domain to your IP and see the camera feed from anywhere in the world through the browser. 

### Next
 - Webcam streaming from browser camera to remote user
