# docker-mirakurun-chinachu on Raspberrypi3 with KTV-FSUSB2N
本家のChinachu with mirakurun on DockerをRaspberry pi 3で動作するように改変しています。
また、それにあたりPT系チューナではなくKEIANのKTV-FSUSB2Nを使用するように変更しています。
テスト環境ではFSUSB2Nは2つ使用し、裏番組録画などをテストしています。
まだデバッグ段階で一般使用に耐えないので、ログ出力が有効になっています。

## できていること
- リアルタイム視聴（XSPFによるストリーム再生及びTVTest+MirakurunBonDriver)
- 録画予約・録画
- 裏番組録画
- 2番組同時視聴
- 視聴中の裏番組録画

## できていないこと
- Chinachuのシステムログが出ない
- チューナーデバイスの検出によりチューナーデバイスのみdockerコンテナと共有
- 番組切り替えを頻繁に行った際のエラー対処
- chinachuでの使用ユーザ、グループの変更
- WebMでのライブ視聴
- 録画済みデータのストリーミング再生

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

### 諸注意
- USBデバイスすべてをｄｏｃｋｅｒコンテナと共有しているのでセキュリティー的に良くありません
- Dockerイメージ内のユーザID/グループIDで設定ファイル及び録画ディレクトリにアクセスできる必要があります
- 同一デバイス、同一コマンドであっても複数使用する場合はmirakurunの設定ファイルには2つチューナーを記述しておかないと裏番組関連の動作を正しく行えません
- チューナーデバイスの接続により、3AのACアダプターを使用していても電力不足に陥るケースがあります

## License
This software is released under the MIT License, see LICENSE.
