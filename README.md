# Guide-For-Scraping-Data-through-Python-Block-some-Special-Token-On-Dynamic-JavaScript-Website-Platform
Target : https://www.mischooldata.org/Legislative/LegislativeDashboard3.aspx
網站解析：
1. ASP.net 撰寫
2. Table內每一個連結都採用 POST BACK
3. 有時候可能會有 unexcepted error 或 session timeout
4. ping 不到其伺服器，但是從 chrome develope Tool 判斷：根據我的網路狀況，平均一個頁面 Loading 要 10-15 秒

目標：
抓取 https://www.mischooldata.org/Legislative/LegislativeDashboard3.aspx
1. #SchoolDistrictBrowser_RadGrid_GridHeader 中的 Table 所有欄位
2. 進到各個 Col:School District Name 進行遍歷
3. 取出 #_LocationHeader、#_Superintendent、#_Mail、#_Phone、#_Email、#_Website
4. 綜合以上內容，建構一 csv

思路：
因為有兩個地方要抓，所以分成兩個階段進行
第一階段：先抓 #SchoolDistrictBrowser_RadGrid_GridHeader 中的 Table
(file : output_Stage1.txt)
第二階段：根據第一階段的結果( 850 筆)資料，分成 850 次進到該頁面取出目標資訊
進到內頁面有兩種方式：
a. 模擬點擊(利用類似按鍵精靈的方式，用 winForm 對著網頁進行點擊)
b. 模擬 Submit Form (FormData 複雜，而且不知道是否有防 Cross-Domain，所以這當做最終方案)
進入到內頁面後，搜尋 #_LocationHeader、#_Superintendent、#_Mail、#_Phone、#_Email、#_Website，並取出其資料
(file : output_Stage2.txt)
第三階段：
讀取 Stage1 和 Stage2 兩個檔案，進行合併，獲得 result.csv

→ Python result for CSV file

因為動態網站裡有很多屏蔽你抓取資料的 token，以上提供了一些在動態網站上如何抓取資料而不容易 GG （有很多亂碼或 Bug 在裡面）的小方法

Output stage 1.

先匯出所有的 #_LocationHeader #_Schools Name 
此時你的 txt會呈現亂成一坨的樣子
						
Output stage 2.					 				
			
再匯出所有「動態」JavaScript 網站上必須要點擊進去才能取得的資料，運用以上這些方法，就可以屏蔽動態網站需要跳轉的 Bug，匯出的資料就不會出現亂碼。
