# docker-mirakurun-chinachu on Raspberrypi3 with KTV-FSUSB2N
本家のChinachu with mirakurun on DockerをRaspberry pi 3で動作するように改変しています。
また、それにあたりPT系チューナではなくKEIANのKTV-FSUSB2Nを使用するように変更しています。

## できていること
- リアルタイム視聴（XPFFによるストリーム再生及びTVTest+MirakurunBonDriver)
- 録画予約・録画
- 裏番組録画
- そのほかChinachuのだいたいの操作

## できていないこと
- 2番組同時視聴
- 録画中のライブ視聴
- 番組切り替えを頻繁に行った際のエラー対処

## Constitution
### Mirakurun
- Alpine Linux 3.6(arm32v6/node:8-alpine)
- [Mirakurun](https://github.com/kanreisa/Mirakurun)
  - branch: master

### Chinachu
- Alpine Linux 3.6(arm32v6/node:8-alpine)
- [Chinachu](https://github.com/kanreisa/Chinachu)
  - branch: gamma

## 動作確認環境
> OS
>>Raspbian stretch lite (2007/11/29)
>> Linux 4.9.59-v7+
>Docker
>>version 18.02.0-ce, build fc4de44  

>Tuner
>>KTV-FSUSB2N(FW書き換え済み)

>Smart card reader
>>KTV-FSUSB2N

## 利用方法
- 最新のdocker & docker-compose がインストール済
- SELinuxの無効化推奨
- ホストマシンのUSBデバイスへのアクセスを追加
```docker-compose.yml
- device:
 - /dev/bus/usb/*:/dev/bus/usb/*
```

- その他の設定は本家に準じます
-- [Chinachu/docker-mirakurun-chinachu: All in one Mirakurun & Chinachu](https://github.com/Chinachu/docker-mirakurun-chinachu)

## License
This software is released under the MIT License, see LICENSE.
