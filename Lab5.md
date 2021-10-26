# Lab 5 - 建立佈建原則

## 建立佈建原則

- 畫面移轉到 Microsoft Endpoint Manager 系統管理中心，點選「裝置」，「Windows 365」，在功能頁籤中選擇「佈建原則」，並點選「建立原則」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/Provisioning1.png "Provisioning1")<br>
- 在頁籤「一般」中，輸入名稱 policy01、選擇內部部署網路連線 OPNC<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/Provisioning2.png "Provisioning2")<br>
- 在頁籤「映像」中，選擇映像類型為自訂映像，選取剛上傳的映像檔 win10-zhtw，如果您想要快速的建立環境讓使用者自行更改設定的話，可以選擇資源庫映像，這部分就不需要建立自訂映像檔<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/Provisioning3.png "Provisioning3")<br>
- 在頁籤「指派」中，選擇您建立的群組，本篇使用 w365_group<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/Provisioning4.png "Provisioning4")<br>
- 在最後一個頁籤「檢閱+建立」中，確認設定無誤後，點選「建立」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/Provisioning5.png "Provisioning5")<br>
- 完成建立後就可以在頁籤「所有雲端電腦」中，看到成功建立 Cloud PC 並且已經指派給使用者 user1<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/Provisioning6.png "Provisioning6")

前往 [Lab 6 - Cloud PC 存取](https://github.com/BrianHsing/Windows365/blob/main/Lab6.md)<br>