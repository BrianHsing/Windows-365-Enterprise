# Lab 2 - 指派授權與設定權限

## 指派授權
- 使用具有全域管理員的帳號登入 「portal.office.com」網址，並且進入 「Microsoft 365 admin center」<br>
- 點選作用中使用者，選擇您所要指派授權的使用者，再「授權與 App 頁籤」中，指派必要的授權，本篇使用 Microsoft 365 F3 搭配 Windows 365 Enterprise 4 vCPU, 16 GB, 128 GB<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/assign.png "assign")<br>
> **請注意，在首次指派之後，系統會自動在作用中使用者的列表中產生 「Windows 365 BPRT Permanent User」使用者帳戶，不要將這個帳戶刪除或是變更，此帳戶可確保 Windows 365 在建置的過程中能順利執行，並不會有任何存取組織的行為** <br>
## 設定 Windows 365 權限
- 訂用帳戶指派讀者角色
  - 使用具有訂用帳戶擁有者與 Azure AD 全域管理員的帳號登入「portal.azure.com」，並且點選訂用帳戶，在右邊功能列選擇「存取控制(IAM)」<br>
    ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/subscription.png "subscription")<br>
  - 點選「新增」，選擇「新增角色指派」<br>
    ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/rbac1.png "rbac1")<br>
  - 在「角色」的頁籤中，選擇「讀者」後，點選下一步<br>
    ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/rbac2.png "rbac2")<br>
  - 在「成員」的頁籤中，選取成員「Windows 365」，點選「檢閱+指派」<br>
    ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/rbac3.png "rbac3")<br>
  - 完成後可以在訂用帳戶的存取控制中，看到讀者權限的資訊<br>
    ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/rbac4.png "rbac4")<br>
- 資源群組指派網路參與者角色
  - 前往資源群組 ADDS，設定存取控制(IAM)，點選「新增」，選擇「新增角色指派」，在「角色」的頁籤中，選擇「網路參與者」後，點選下一步<br>
    ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/rbac5.png "rbac5")<br>
  - 在「成員」的頁籤中，選取成員「Windows 365」，點選「檢閱+指派」<br>
    ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/rbac3.png "rbac3")<br>
  - 完成後可以在資源群組的存取控制中，看到網路參與者權限與繼承讀者的資訊<br>
    ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/rbac6.png "rbac6")<br>

前往[Lab 3 - 建立虛擬網路連線至模擬的環境](https://github.com/BrianHsing/Windows365/blob/main/Lab3.md)<br>