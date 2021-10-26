# Lab 3 - 建立虛擬網路連線至模擬的環境

## 建立內部部署網路連線

- 使用具有全域管理員的帳號登入 「portal.office.com」網址，並且進入 「Microsoft 365 admin center」，在左邊功能分類系統管理員中心選擇「端點管理員」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/deploy1.png "deploy1")<br>
- 進入後，選擇「裝置」，並且選擇 「Windows 365」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/deploy2.png "deploy2")<br>
- 點選頁籤「內部部署網路連線」，並且點選「建立」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/deploy3.png "deploy3")<br>
- 在頁籤「網路詳細資料」中，您需要填幾個資訊：<br>
  - 名稱：您所建立這個內部部署網路連接設定的唯一名稱<br>
  - 訂用帳戶<br>
  - 資源群組：本範例使用稍早建立的 ADDS <br>
  - 虛擬網路：本範例使用稍早建立的 ADDS-vnet<br>
  - 子網路：本範例使用稍早建立的 w365-subnet<br>
  - 完成後點選「下一個」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/opnc1.png "opnc1")<br>
- 在頁籤「AD 網域」中，您需要填幾個資訊：<br>
  - AD DNS 網域名稱：您需要填入您 AD DNS 名稱，本範例使用 brianhsing.club<br>
  - 組織單位：本範例使用 OU=W365,DC=brianhsing,DC=club，如果您是建立其他 OU 放置，您必須確保此 OU 有被勾選與 Azure AD 同步，如果沒有勾選，會造成失敗<br>
  - AD 使用者名稱 UPN：您可以使用一個已加入網域的使用者帳號即可<br>
  - AD 網域密碼：輸入使用者帳號的密碼<br>
  - 確認 AD 網域密碼：再次輸入<br>
  - 完成後點選「下一個」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/opnc2.png "opnc2")<br>
 - 完成後請點選「檢閱+建立」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/opnc3.png "opnc3")<br>
 - 完成後可以看到您建立的內部部署網路連線，可以點選狀態，檢查並更改一些資訊<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/opnc7.png "opnc4")<br>
 - 透過 Watchdog Service，您可以很容易地觀察到目前您的環境健康狀況<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/opnc8.png "opnc5")<br>
 - 在屬性的頁籤您也可隨時變更您的 Azure 相關資源與 AD 網域的資訊<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/opnc6.png "opnc6")<br>

前往[Lab 4 - 建立自訂映像檔](https://github.com/BrianHsing/Windows365/blob/main/Lab4.md)<br>