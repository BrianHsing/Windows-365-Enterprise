# MSIX 應用程式指派

## 前置作業
- 在 Microsoft Endpoint Manager 系統管理中心中，主要支援幾種檔案格式，能讓您派送至 Cloud PC 中，本篇主要是示範如何透過 MSIX 格式來派送您的應用程式，在這之前您必須先準備兩件事情：<br>
  - 建立自我簽署憑證：本篇提供 [msix.cer] (https://github.com/BrianHsing/Windows365/blob/main/msix.cer) 讓您能夠進行練習<br>
  - 重新封裝您的應用程式：本篇提供 [notepad++](https://github.com/BrianHsing/Windows365/blob/main/notepadpp_1.0.0.0_x64__s1mw6y3htna62.msix) 讓您能夠進行練習<br>
您可前往 [了解 MSIX 應用程式連接與 MSIX 映像檔準備](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/MSIX-package.md) 了解如何準備這些事情<br>

## 設定組態設定檔

- 畫面來到 Microsoft Endpoint Manager 系統管理中心，點選「裝置」後，選擇「組態設定檔」後，點選「建立設定檔」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix1.png "msix1")<br>
- 平台選擇 「Windows 10 及更新版本」，設定檔類型選擇「範本」，在範本列表中選擇「信任的憑證」後，點選「建立」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix2.png "msix2")<br>
- 在頁籤「基本」中，輸入名稱，完成後選擇「下一頁」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix3.png "msix3")<br>
- 在頁籤「組態設定」中，選擇您剛下載的「msix.cer」，目的地存放區選擇「電腦憑證存放區 - 根」，完成後選擇「下一頁」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix4.png "msix4")<br>
- 在頁籤「指派」中，包含的群組選項，新增群組 w365_group，完成後選擇「下一頁」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix5.png "msix5")<br>
-  在頁籤「適用性規則」中，將條件設定只套用在 Windows 10/11 企業版，完成後選擇「下一頁」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix6.png "msix6")<br>
-  在頁籤「檢閱+建立」中，檢視設定的資訊無誤後，點選建立<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix7.png "msix7")<br>
## 新增 Windows 應用程式

- Microsoft Endpoint Manager 系統管理中心，點選「應用程式」後，依平台的功能列中選擇 Windows<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix8.png "msix8")<br>
- 點選「新增」後，應用程式類型選擇「企業營運應用程式」，點選「選取」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix9.png "msix9")<br>
- 在頁籤「應用程式資訊」中，選取您剛下載的檔案「notepadpp_1.0.0.0_x64__s1mw6y3htna62.msix」，點選「確定」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix10.png "msix10")<br>
- 在這裡會需要您填入名稱、描述、發行者，完成後點選「下一頁」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix11.png "msix11")<br>
- 在頁籤「指派」中，將群組 W365_group 加入後點選「下一頁」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix12.png "msix12")<br>
- 確認資訊無誤後，點選「建立」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/msix13.png "msix13")<br>

## 驗證是否有成功派送應用程式

