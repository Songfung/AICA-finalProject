# LipReading_FinalProject
## Project 描述
唇語辨識密碼鎖：想要解鎖時在有人的情況下能降低暴露密碼的風險，且能免除按密碼的不便利性。

### Project Scope 
- 紅外線偵測與臉部辨識
- 辨識唇形
- 轉成文字檔
- 利用樹莓Pi辨識文字檔，若符合密碼則開鎖
- 固定位置
- 單一人臉



### Target Audience
- 對於密碼的隱蔽性有高要求與強調便利開鎖的使用者



### Constraints 
- 英文(數字、單字、句子) 
- 長度適中
- 正面對著鏡頭
- 固定距離
- 一句話講完



## Project Decomposition and Planning
- 偵測臉部是否在正確位置
- 錄影使用者的唇形
- 模型辨識唇形是哪些字
- 樹莓Pi辨識文字檔與密碼是否相符
- 若相符則通電使電子鎖開啟
- ( 建立字彙資料庫, 訓練LipNet模型 ) - 如果需要training model的話



## Project Expectation



1. Project Focus
- 偵測臉部位置盡量精準
- 脣形辨識準確率盡量提高
- LipNet在RPi的implementation (by docker)
- 辨識文字檔與儲存文字檔系統 
- 正確implement電路




2. What does your application look like? 

- 紅外線偵測是否有人在前面，開啟RPI人臉辨識，偵測臉部停留幾秒，打開Pi-camera錄影功能，並固定在一個位置(**實際操作後會決定固定的位置**)，以筆電連線RPi並再使用該功能時能顯示camera的即時影像，講完密碼後人臉離開表示錄影結束，將影片檔input到LipNet並辨識，若成功顯示成功並開鎖，若失敗則顯示密碼不正確。




3. How are you going to test your application?
- 辨識率, 確認唇語符合使用者的語意，辨識正確的字數比例(or CER,WER)
- 紅外線正確辨識距離
- 人臉辨識程式正確辨識
- 電路正確通電開鎖




## Solution Proposals
- 利用樹莓pi辨識人臉以及脣形並辨識密碼是否正確，如正確則開鎖。



## ALGORITM



- 使用字彙資料庫 LRW

- 使用LipNet作為我們的AI辨識

- 查看論文以最佳化LipNet model



### Workflow

- 1.紅外線偵測使用者站到固定位置


- 2.開啟臉部辨識程式(此時mobaxterm開啟Pi-camera偵測影像)


- 3.若辨識臉部在正確範圍數秒則開始錄影(此時mobaxterm顯示開始錄影)


- 4.使用者在講完密碼後將臉部移開鏡頭


- 5.臉部辨識程式此時偵測到臉部不在正確範圍內時則關閉此程式並停止錄影

- 6.紅外線停止偵測到門鎖解開後數秒或辨識密碼錯誤

- 7.將影片檔input進LipNet辨識

- 8.辨識出的文字檔若 (1)與密碼相符合則mobaxterm顯示密碼正確並通電開鎖 (2)不符合則mobaxterm顯示密碼錯誤

- 9.將影片檔刪除

- 10.紅外線重新開啟偵測功能

---
