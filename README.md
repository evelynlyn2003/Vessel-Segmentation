



#  CNN的語意切割辨識糖尿病視網膜病變病灶影像，進行嚴重度分析

- 專案使用卷積神經網路（Convolutional Neural Network, CNN）的語義分割技術，精準辨識糖尿病視網膜病變（Diabetic Retinopathy, DR）影像中的所有核心病灶。
模型採用 UNet深度學習架構，利用其跳躍連接機制，有效恢復了分割結果的細節。為了處理病灶與背景之間的類別不平衡問題，採用 Dice Loss 進行優化，並透過資料增強提升模型的泛化能力。
 
### A. 數據 (Dataset & DataLoader)

#### 1. 資料來源
[https://www.kaggle.com/competitions/sai-vessel-segmentation2/submissions]


#### 2. 數據(Dataset & Dataloader)

訓練集：16張。(調整權重 (W))


驗證集:  4張。(調整超參數 (H))

測試集:  20張。 (報告最終性能 )

影像增強 : 使用 Albumentations

---

### B. 模型 (Model)

#### 1. 使用UNet來做語義分割 (Semantic Segmentation)

2.解碼器:* 跳躍連接 (Skip Connection)： 使用 torch.cat 將編碼器的高解析度特徵與解碼器特徵融合，保留邊緣細節。


---

### C. 訓練與優化 (Training)

#### 1. 損失函數

`-DiceLoss` (Dice 損失)：

*核心作用： 不計算像素的絕對差異，而是直接量化模型預測遮罩與真實標籤遮罩之間的重疊度。

*優勢： 對前景類別（即微小病灶像素）的錯誤更敏感，有效解決了糖尿病視網膜病變 (DR) 圖像中病灶像素極少的問題。

*實作： 使用 fusionlab 庫進行簡化實作。

`-DiceScore` (Dice 相似係數 DSC)：

*作用： 作為獨立的性能評估指標，衡量分割的準確性。DiceScore 的值越高（越接近 1），表示分割重疊度越高，性能越好。

---

### D. Kaggle成績
1. Kaggle Public Score : 0.76163
   
ˋ------ Advanced Baseline -----0.80102ˋ

ˋ------ baseline ---------------0.59445ˋ






