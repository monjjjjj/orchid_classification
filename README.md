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
