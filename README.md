# orchid_classification
## 蘭花資料集分類訓練
### 遇到的困難
此次在蘭花分類的練習當中，在讀圖片檔的時候有遇到了一些困難！  

#### 困難1  
因為一開始想說圖片量蠻大的，所以想要在自己的電腦上用pycharm跑，但執行起來速度很慢，且目前在實驗室中尚未分配到桌機～  
因此後來改在colab上執行，並且讀取google drive中的training data！  
#### 困難2
從google drive中讀取資料遇到了困難，在確認colab有mount到drive且路徑是正確的前提下，colab一直無法讀取圖片檔！  
一開始以為是檔案有問題，所以做了確認資料夾裡都是jpg檔並且排除csv檔，但仍然讀不到檔案！  
讀檔的問題卡了兩天之後，詢問同學並且與同學一起trace code，最後發現資料夾路徑必須是放在雙引號內，而非單引號內（但pycharm用單引號就可以！）！  
排除問題之後終於能夠繼續往下走！ 

#### 困難3
欲將training data提取20%的資料來做validation data，但蘭花資料集每個類別只有10張照片，如果提取20%的話代表每個類別只提取了兩張照片！    
因為有提取一部分的training data來做validation data，所以有對剩下80%的training data做資料增補！  
結果顯示validation的準確度是很低的（大概在50~60%之間跳動），loss也降不下來～  
與其他人討論的結果，我們認為有可能是validation data的資料量不夠多，因而導致上述結果的產生！  

### 訓練過程說明
- 使用ResNet50及ResNet152來訓練模型，並且比較結果  
- 除了使用ResNet外，也有使用VGG16去做訓練，在相同的資料條件之下，結果並不是很好！
- 嘗試將一部分的training data拿來做validation data，但目前看起來效果並不是很好。
- 嘗試將一部分的training data分割出來當作validation data，並且使用data augmentation來增加training data的資料量！


### Result of ResNet50
#### Model accuracy
![ResNet50_acc](https://user-images.githubusercontent.com/62006029/192693277-c40b3b15-5bc5-4835-b07e-bf1afcb45301.png)
#### Model loss
![ResNet50_loss](https://user-images.githubusercontent.com/62006029/192693302-90b27bd8-5080-4652-98dd-544c19aa6669.png)

### Result of ResNet152
#### Model accuracy
![ResNet152_acc](https://user-images.githubusercontent.com/62006029/192693166-b9e1708f-265a-44bd-a79b-39d0b58c680d.png)
#### Model loss
![ResNet152_loss](https://user-images.githubusercontent.com/62006029/192693174-d6d15637-80b1-42be-a340-438422bc54f6.png)

### Comparison
#### Model accuracy
![2model_acc](https://user-images.githubusercontent.com/62006029/192693721-8a73eada-d29e-418c-bcf3-19e5f02def85.png)
#### Model loss
![2model_loss](https://user-images.githubusercontent.com/62006029/192693767-aed7ac87-3ee8-47db-a5d8-fdfb0c100aa6.png)

### Summary
由上圖可觀察到ResNet50的收斂速度比ResNet152還要快，此結論為合理的！  
因ResNet152的參數量是ResNet50的2.5倍，因此收斂速度較慢是正常的。  
儘管收斂速度較慢，但兩者最後的準確度是差異不大的，因此以蘭花分類來看的話，使用ResNet50即可！  

---

在ResNet出現之前，做image classification是使用VGG16，因此在相同的資料集下，想試試看使用VGG16做Training！  
### Result of VGG16
#### Model accuracy
![VGG16_acc](https://user-images.githubusercontent.com/62006029/193499979-17bb32f5-9c65-4f05-b8ee-fd5f2b00af3b.png)
#### Model loss 
![VGG16_loss](https://user-images.githubusercontent.com/62006029/193500098-8e4501bf-ff4c-465b-b9f4-a9124f1a52eb.png)

### Summary
在相同的資料集下，VGG16要訓練30 epochs才會收斂，收斂速度遠低於ResNet！  
從training history來看，過程也比較不穩定！


---
## 分割20%的training data來做validation data (使用ResNet50)
80% training data, 20% testing data
### Result
#### Model accuracy
![ResNet50_val_acc](https://user-images.githubusercontent.com/62006029/193730136-473be82c-bc14-4175-9eb5-28a0d7250888.png)
#### Model loss 
![ResNet50_val_loss](https://user-images.githubusercontent.com/62006029/193730236-cd8adb16-9441-41fb-80e3-204bbb571c91.png)

### Summary
使用20%的訓練資料來當作驗證資料，但結果幾乎是沒有收斂（accuracy: 0.34246575832366943）  
也許每個類別的testing data真的太少了，但原本想說如果我也將testing data做資料增補會不會有幫助！  
結果看起來如果將testing data做資料增補後去做training，結果更差！  
詢問了其他人的意見後，才知道原來一般不會將testing data或validation data去做資料增補，會希望使用原圖去做validation！
因為做了資料增補過後的圖有一定的失真度，可能會讓驗證結果變得更差！
