# Lab 4 - 建立自訂映像檔

此 Lab 是要示範如何讓使用者進入 Cloud PC 時，就能夠直接使用熟悉的語言介面<br>

## 建立虛擬機器
- 在搜尋列搜尋虛擬機器，並且選擇虛擬機器 <br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/vm1.png "vm1")<br>
- 點選「建立」，選擇「虛擬機器」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/vm2.png "vm2")<br>
- 在建立虛擬機器的細節中，最重要的部分，請選擇影像為 Windows 10/11 Enterprise，本篇選擇 Windows 10 Enterprise, Version 20H2 - Gen2 進行操作，剩下的部分您可以將此虛擬機器放在稍早建立的虛擬網路內中，就不在細說<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/vm3.png "vm3")<br>
> **建立虛擬機器的詳細過程可以參閱官方文件教學說明 https://docs.microsoft.com/zh-tw/azure/virtual-machines/windows/quick-create-portal <br>

## 安裝 Windows 365 Language Installer (only Windows 10)

- 開啟您剛建立的虛擬機器後，開啟 PowerShell，並輸入`Install-Script -Name Windows365LanguagesInstaller`，並且所有的要求輸入，均輸入 Y<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ps4.png "ps4")<br>
- 在 PowerShell 輸入 `Windows365LanguagesInstaller.ps1`<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ps5.png "ps5")<br>
- 輸入您要安裝語言的對應號碼，每安裝一次語言都需要重新執行 `Windows365LanguagesInstaller.ps1`，本篇選擇安裝 Chinese (Traditional)，輸入後就會進行自動安裝，安裝會需要一些時間，請耐心等待一下<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ps6.png "ps6")<br>

## 建立自訂映像檔

- 完成您所需要的語言安裝後，使用同樣的 Powershell，輸入`C:\Windows\System32\Sysprep\sysprep.exe /oobe /generalize /shutdown`，之後會執行一般化並關機<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ps7.png "ps7")<br>
- 確認虛擬機器狀態為已停止，點選上方功能列「擷取」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/capture1.png "capture1")<br>
- 在「共用映像至共用映像庫」的選項中，選擇否，只擷取受控映像，輸入名稱後，點選「檢閱+建立」，下個頁面再點「選立」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/capture4.png "capture3")<br>

## 新增 Windows 365 裝置映像

- 畫面移轉到 Microsoft Endpoint Manager 系統管理中心，點選「裝置」，「Windows 365」，在功能頁籤中選擇「裝置映像」，並點選「新增」。在右方窗格填上名稱、映像版本、選取剛建立的自訂映像檔後，點選「新增」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/image1.png "image1")<br>
- 完成後即可看到顯示在列表中<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/capture5.png "capture5")<br>

# 建立 Group Policy

- 將畫面一致您稍早建立的 ADDS VM 內的畫面，開啟 Group Policy Management<br>
![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo1.png "gpo1")<br>
- 在 W365 OU 點選右鍵，點選 「Create a GPO ...」<br>
![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo2.png "gpo2")<br>
- 輸入 New GPO 名稱<br>
![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo3.png "gpo3")<br>
- 在剛剛建立的 GPO 上點選右鍵，選擇 Edit...<br>
![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo4.png "gpo4")<br>
- 點選 User Configuration，選擇 Preferences，選擇 Windows Settings 後，右鍵點選 Registry，並且選擇 New，Registry Item<br>
![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo5.png "gpo5")<br>
- 看到 New Registry Properties 畫面後，請參考以下資訊更改：<br>
  - Action：Replace<br>
  - Hive：HKEY_CURRENT_USER<br>
  - Key Path：Control Panel\Desktop<br>
  - Value name：PreferredUILanguages<br>
  - Value type：REG_SZ<br>
  - Value data：zh-TW<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo6.png "gpo6")<br>
- 完成後再點選頁籤 「Common」，請勾選以下選項<br>
  -  logged-on user's security context (user policy option)<br>
  -  Apply once and do not reapply：此項目可確保使用者可自行更換語言<br>
  -  Item-level targeting<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo7.png "gpo7")<br>
  - 點選 「Targeting...」後，點選 「New Item」會展開列表，這時再點選「Security Group」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo8.png "gpo8")<br>
  - 在這之前，如果您沒有安全性群組，會需要您建立一個安全性群組，裡面要包含 User1<br>
  - 本篇選擇建立好的 Security Group 「w365_group」，下方選項選擇「User in group」後，點選 ok<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo9.png "gpo9")<br>
- 畫面再回到 Group Policy Management Editor，在導航列選擇 User Configuration，選擇 Preferences，點選 Control Panel Settings 後，在 Regional Options 上點選右鍵，選擇 New，點選 Regional Options <br>
![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo10.png "gpo10")<br>
- 將下方 User Locale 的下拉式選單選擇 Chinese (Traditional, Taiwan) 後，按下 F5，您會看到下方有一條綠色的線，還未按下 F5 時，呈現紅色線條<br>
![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo11.png "gpo11")<br>
-  完成後再點選頁籤 「Common」，請勾選以下選項<br>
  -  logged-on user's security context (user policy option)<br>
  -  Apply once and do not reapply：此項目可確保使用者可自行更換語言<br>
  -  Item-level targeting<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo7.png "gpo7")<br>
  - 點選 「Targeting...」後，點選 「New Item」會展開列表，這時再點選「Security Group」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo8.png "gpo8")<br>
  - 在這之前，如果您沒有安全性群組，會需要您建立一個安全性群組，裡面要包含 User1<br>
  - 本篇選擇建立好的 Security Group 「w365_group」，下方選項選擇「User in group」後，點選 ok<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo9.png "gpo9")<br>
- 全部完成後，開啟 CMD，輸入`gpupdate /force`<br>
![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/gpo12.png "gpo12")<br>

前往 [Lab 5 - 建立佈建原則](https://github.com/BrianHsing/Windows365/blob/main/Lab5.md)<br>
