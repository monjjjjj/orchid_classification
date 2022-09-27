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

### 訓練過程說明
- 使用ResNet50及ResNet152來訓練模型，並且比較結果！
- 嘗試將一部分的training data拿來做validation data，但目前看起來效果並不是很好。
- 一樣將一部分的training data分割出來當作validation data，並且使用data augmentation來增加training data的資料量！


### Result of ResNet50
#### Model accuracy
![acc](https://user-images.githubusercontent.com/62006029/192515160-2cf0c59f-e58b-4353-8230-15a2f880ba51.png)
#### Model loss
![loss](https://user-images.githubusercontent.com/62006029/192515201-5cd482b6-59dd-4a5b-841d-0b64647fb1cf.png)
