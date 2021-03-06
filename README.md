# Stock-prediction
## Abstract
AI 發展時至今日，在分群和辨識系統上已經做得很好了，人臉辨識、遊戲甚至是遠超人類，然而，在金融上的成就遠遠不及其他領域，也許是因為財金這塊領域的 domain knowledge太深，導致模型在基礎設定上本來就考慮的不夠周全，因此我希望能運用機器學習看看 ML 是否能幫助股票分析。
## Motivation
個人利益方面，當然是希望所學能幫自己賺錢。社會方面，因為 AI在有些方面已經超越人類了，像是圍棋，而運用在財金方面是否能有顯著的提供協助?財金相較於其他領域是更貼近人們的生活的，因此可能對人類的生活產生巨變，而且投資要考量的變數實在很多，所以我很好奇運用 AI 技術的投資能否打敗人類。

AI 已經有發展到一定的程度了，然而運用 AI 的領域實在不算多，目前可能只有遊戲、視覺、跟自然語言處理有比較傑出的成果，AI 勢必還需要在某些能大大改變人們生活的領域發展，更能顯的 AI 會如何影響人類。如果 AI 加上財金將會大大地改變人們的生活，而且投資並不是只有考量數學，還是一門跟人文、心理相關的學問，而 AI 是否能連這些都考慮到是我所好奇的。
## Introduction
在 AI 在其他領域有不凡的成就時，很多資料分析師都有個疑問，像是財金那麼複雜且和人們息息相關的領域，ML 有辦法去輔助人們做出決策嗎?以下是很多國外學者在股票分析上的成果，而我想看看當分析的資料不是全世界，而是僅僅是台灣時，會發生什麼事情?畢竟一般的台灣人通常只在乎國內的情形，很少對國外的金融商品下手。如果下列的成果都那麼好，那台灣的資料也會一樣好嗎?所以我會透過技術面去預測及分析股價。
## Related Work 
*	["Global stock market investment strategies based on financial network indicators using machine learning techniques. "](https://www.sciencedirect.com/science/article/abs/pii/S0957417418305761) Lee, Tae Kyun, et al. "Global stock market investment strategies based on financial network indicators using machine learning techniques." Expert Systems with Applications 117 (2019): 228-242.
*	["Supporting Investment Management Processes with Machine Learning Techniques."](https://www.researchgate.net/profile/Martin_Sedlmayr/publication/221200937_Unterstutzung_medizinischer_Leitlinien_-_Von_der_zielorientierten_Modellierung_zur_proaktiven_Assistenz/links/0a85e531c2277cd61d000000.pdf#page=275) Groth, Sven S., and Jan Muntermann. "Supporting Investment Management Processes with Machine Learning Techniques." Wirtschaftsinformatik (2). 2009.
*	["A machine learning model for stock market prediction."](https://arxiv.org/ftp/arxiv/papers/1402/1402.7351.pdf) Hegazy, Osman, Omar S. Soliman, and Mustafa Abdul Salam. "A machine learning model for stock market prediction." arXiv preprint arXiv:1402.7351 (2014).
*	["Predicting stock and stock price index movement using trend deterministic data preparation and machine learning techniques."](https://www.sciencedirect.com/science/article/pii/S0957417414004473) Patel, Jigar, et al. "Predicting stock and stock price index movement using trend deterministic data preparation and machine learning techniques." Expert systems with applications 42.1 (2015): 259-268.
*	希望能用台灣的股票資料，做出和上述差不多好的結果
## Methodology
### Problem statement - Technical analysis
1. 起始金額為現金 10,000 元，希望最後能賺最多錢
2. 每天都要判斷買多還是賣多這固定的十檔股票(0050、0056、鴻海、台積電、聯發科、大立光、富邦金、國泰金、玉山金、元大金)
3. 自變數會用先前的開盤價、最高價、最低價、收盤價、成交量、5 日均價、20 日均價、網路聲量(如果有學會爬蟲的話)等等，而變數就是這十檔分別該買還是賣
4. 假設想買一定買得到，想脫手一定賣得掉
5. 假設股票能以前一天的收盤價買進，融券也是以前一天的收盤價為代價
6. 假設手續費為交易金額的 0.1%
7. 先預測哪些會漲那些會跌之後，先將現金 10,000 元保留以備不時之需。在認為漲超過手續費的股票中，覺得投資報酬率最高的投入剩餘現有現金的 50%，第二高的再投入剩餘現有現金的 50%，以此類推，並將剩餘所有的現有現金投入投資報酬率最低但還是認為能漲超過手續費的，然後隔天要將所有持有的股票都賣掉。認為會跌超過手續費的也是按照買股的方式，在認為跌超過手續費的股票中，覺得賣空的投資報酬率最高的就借價值約為現有現金的 50%的券，賣空的投資報酬率第二高的再借價值約為剩餘現有現金的 25%的券，以此類推，並在最後借與前一個同價值但還是認為能跌超過手續費的券，然後隔天也要將所有持有的股票都賣掉。隔天都會平倉。
8. 可以全部都不買也不賣
### Baseline Method 
* 將所有的變數拿去跑回歸，並預測報酬率
* 預測股價與目前股價做比較
* 每一次都是研究 30 天的資料決定第 31 天的買賣
* Testing data 也是 30 天
### ML Method 
* 利用 PCA 找出重要參數，並且減少運算量
* 跑 SVM 和 DNN，並預測報酬率
* 預測股價與目前股價做比較
* 每一次都是研究 30 天的資料決定第 31 天的買賣
* Testing data 也是 30 天
### 超參數設定
#### PCA: 
* n_components = 24
#### DNN: 
* hidden layer 1: 10 neurons, selu
* hidden layer 2: 10 neurons, relu
* output layer: 1 neurons 預測報酬率
* 用 selu 和 relu 因為是線性關係
* loss: mse optimizer: adam metrics: mae
## Data
data source: TEJ, yahoo finance, apple stock
會先將.csv 下載下來後，再使用 pandas, numpy 等進行 EDA
### stock
* 0050 Yuanta Taiwan Top5: 0050 元大台灣 50
* 0056 PTD: 0056 元大高股息
* 2317 Hon Hai Precision:2317 鴻海
* 2330 TSMC: 2330 台積電
* 2454 MediaTek: 2454 聯發科
* 3008 Largan: 3008 大立光
* 2881 Fubon FHC: 2881富邦金
* 2882 Cathay Holdings:2882 國泰金
* 2884 E.S.F.H: 2884 玉山金
* 2885 Yuanta Group:2885 元大金
### attribute
* CO_ID: 公司代碼
* Date: 年月日
* Open(NTD): 開盤價(元)
* High(NTD): 最高價(元)
* Low(NTD): 最低價(元)
* Close(NTD): 收盤價(元)
* Volume(1000S): 成交量(千股)
* Amount(NTD1000): 成交值(千元)
* AVG CLOSE: 當日均價(元)
* AVG CLOSE 5D: 5 日均價(元)
* AVG CLOSE 10D: 10 日均價(元)
* AVG CLOSE 20D: 20 日均價(元)
* AVG Vol 5D: 5 日均量
* AVG Vol 10D: 10 日均量
* AVG Vol 20D: 20 日均量
* ROI%: 報酬率％
* Shares(1000S): 流通在外股數(千股)
* Market Cap.(NTD MN):市值(百萬元)
* P/E-TEJ: 本益比-TEJ
* P/B-TEJ: 股價淨值比TEJ
* Dividend_Yield%: 股利殖利率
* Cash_Dividend%: 現金股利率
* Price_Change(NTD): 股價漲跌(元)
* High minus Low %: 高低價差%
* Market: 上市別
* Capital: 資本
* No.of Employee: 員工人數
### EDA(Exploratory Data Analysis)
* 使用 pandas
* 將每筆資料從只看 1 天變成看 30 天
* 將不重要的 attribute drop 掉( 'CO_ID’, 'Date’, 'Market’, ‘ROI’)
* 要預測的 y 是‘ROI’，也就是報酬率
* 將資料分為 train 和 test(一個月)
![](https://user-images.githubusercontent.com/43957213/126780430-79530b63-9418-431a-b5c7-5aa9288b2ddc.png)
![](https://user-images.githubusercontent.com/43957213/126780805-81363837-2558-4a4a-8368-409bdf277fd0.png)

![](https://user-images.githubusercontent.com/43957213/126780811-a0542c2b-44a1-4853-9f26-370770e9ce3e.png)

![](https://user-images.githubusercontent.com/43957213/126780816-2a4038b6-12d8-4e34-be04-1432f8f3701e.png)

![](https://user-images.githubusercontent.com/43957213/126780820-53b20c05-2276-42c4-954a-e1ce9dd0f87f.png)
![](https://user-images.githubusercontent.com/43957213/126780823-6e5ed466-794b-4213-9b7b-ea2667e1949b.png)
![](https://user-images.githubusercontent.com/43957213/126780834-061740d9-6617-4b69-95e1-50dacdc37a46.png)
![](https://user-images.githubusercontent.com/43957213/126780840-671936e3-2f43-4153-9834-8b6b42981333.png)
![](https://user-images.githubusercontent.com/43957213/126780843-bab126fd-e4f9-405b-b97f-fd481833e1f4.png)
![](https://user-images.githubusercontent.com/43957213/126780856-e5b22a14-3f98-4fd3-9362-d8c8ab46cf1c.png)
![](https://user-images.githubusercontent.com/43957213/126780864-dae6cc5d-b3c5-4a7d-a654-d70175ed99de.png)
![](https://user-images.githubusercontent.com/43957213/126780866-51626aa1-622d-406d-bc5b-bdd3a74c683a.png)
![](https://user-images.githubusercontent.com/43957213/126780876-4cd4ae7a-2068-41ad-ba92-2cac662727cc.png)
## Results
final money with regression: 11025.41257057684

final money with svm: 11424.564134181688

final money with dnn model: 11720.512937545913

只用 30 都能從 10000 賺到 11000 以上，可以看出三種模型都是有幫助的，也能看出 ML 和 DL 的確是有用的技術，能幫助我們賺更多錢，因為基本上賺的都比儲蓄高，可以認為對預測買賣是有一定的效力的。
## Conclusion
因為完全沒有人為因素，且流通性假設為很高，所以才能賺到這個數字，也代表了少了很多人為影響決策的因素，散戶也能透過智慧理財賺錢，而這是在相對保守的投資策略下賺錢，也許更激進點的能夠賺一大筆錢。
## Future Use
希望能透過更多 ML 的方法，甚至是 DL 和 RL 的方法，讓成果變得更好，未來也會考慮考量更多變數並篩掉不太有解釋效用的變數，也希望未來能不僅僅從技術面分析，也考量到基本面分析，這樣不僅能做的更全面，也更能分辨哪些因素才是重要因子，又或是透過文字探勘蒐集其他有效的資訊，也期許未來能考量更多市場機制，例如流動性等等。
