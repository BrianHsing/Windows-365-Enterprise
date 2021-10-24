# Lab 1 - 模擬地端 Windows AD 與網路環境

## 使用 CloudShell 建立 Azure VM ADDS 與網路環境

 - 下載 [Single-ADDS.ps1](https://github.com/BrianHsing/Windows365/blob/main/Single-ADDS.ps1)<br>
	- 此命令會建立：<br>
    	- 資源群組 ADDS-rg，並且將資源都放置在東亞<br>
    	- 建立一台規格為 D4sv3 的虛擬機器 ADDS，私人 IP 指派靜態 172.16.1.4<br>
    	- 虛擬網路的網路位址為 172.16.0.0/16，分別建立三個子網路：<br>
        	- adds-subnet 172.16.0.0/16，用於放置 ADDS 或其他 Server Farm 的虛擬機器<br>
        	- w365-subnet 172.16.2.0/24，用於稍後建置 Windows 365 企業版所指派的子網路<br>
        	- AzureBastionSubnet 172.16.3.0/24，用於建置 Azure Bastion 必須的子網路<br>
    	- 堡壘 (Azure Bastion)<br>
- 使用 Single-ADDS.ps1 佈署 Windows ADDS Server <br> 
	- 啟用 CloudShell<br>
    - 輸入`Connect-AzAccount` 登入<br>
	- 上傳 Single-ADDS.ps1<br>
	![GITHUB](https://github.com/BrianHsing/Azure-Migrate/blob/master/hyper-v/image/cloudshell-uploadps1.PNG "cloudshell-uploadps1")<br>	  
	- 輸入並執行 `./Single-ADDS.ps1` <br>
    ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/upload.png "upload-succsess")<br>
- 設定虛擬網路DNS 伺服器 ADDS-vnet 指向 172.16.1.4<br>
   ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds1.png "adds1")<br>
 - 進入虛擬機器設定 Active Directory 網域服務 <br> 
	- 進入 Azure Portal，選擇虛擬機器 ADDS，使用 Bastion 連線 (isadmin/isadmin@123) <br>
	  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds2.png "adds2")<br>
	- 開啟伺服器管理員 (Server Manager)，點選 Promote this server to a domain controller<br>
	  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds3.png "adds3")<br>
	- 點選 Add a new forest，並輸入 Root domain name，此範例先設定 brianhsing.club，後續再做 AAD Connect 時，就不需要再另外設定 UPN 尾碼。<br>
	> **Tips.請不要使用結尾為「.local」的網域，此網域無法在虛擬網路內路由** <br>
	
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds4.png "adds4")<br>
	- 自行輸入 Directory Services Restore Mode 密碼<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds5.png "adds5")<br>
	- DNS Option 直接選擇下一步<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds6.png "adds6")<br>
	- Additional Option 直接選擇下一步，稍後登入會使用 NETBIOS\isadmin 帳號格式<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds7.png "adds7")<br>
	- Path 直接選擇下一步。如果是正式環境，建議將這三個資料夾與系統磁區分開<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds8.png "adds8")<br>
	- Review Option 下一步後，Prerequisites Check 頁面選擇 Install，等待安裝結束後，會自動開機。<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds9.png "adds9")<br>
	- 使用 Bastion 連線 (您設定的NetBios\isadmin / isadmin@123)<br>
	- 開啟 Active Directory Users and Computers <br>
	- 建立組織單位 (organizational unit) AVD<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds10.png "adds10")<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds11.png "adds11")<br>
	- 建立使用者物件 user1、user2、user3<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds12.png "adds12")<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds13.png "adds13")<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds14.png "adds14")<br>
	 ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/adds15.png "adds15")<br>

## 設定 Azure AD Connect & Azure AD Hybrid Join

- Azure AD Connect v2 的版本強制使用 TLS 1.2，所以您必須要確保您有啟用 TLS 1.2，您可以使用下列 PowerShell 指令碼，在 Azure AD Connect 伺服器上啟用 TLS 1.2<br>
 ````
    New-Item 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null

    New-ItemProperty -path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -name 'SystemDefaultTlsVersions' -value '1' -PropertyType 'DWord' -Force | Out-Null

    New-ItemProperty -path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null

    New-Item 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null

    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SystemDefaultTlsVersions' -value '1' -PropertyType 'DWord' -Force | Out-Null

    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null

    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null

    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value '1' -PropertyType 'DWord' -Force | Out-Null

    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 0 -PropertyType 'DWord' -Force | Out-Null

    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null

    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value '1' -PropertyType 'DWord' -Force | Out-Null

    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 0 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.2 has been enabled.'
 ````
 - 在 Server Manager 視窗中，選擇 Local Server，將 IE Enhanced Security Configuration 設定調整為 Off<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/aad1.png "add1")<br>
 - 開啟 IE 瀏覽器，輸入 https://go.microsoft.com/fwlink/?LinkId=615771 ，並下載。<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add2.png "add2")<br>
 - 開啟 AzureADConnect.exe 安裝<br>
 - 勾選「I agree to the License terms and privacy notes.」，點選「Continue」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add3.png "add3")<br>
 - 選擇「Customize」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add4.png "add4")<br>
 - 選擇「Install」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add5.png "add5")<br>
 - 選擇「Password Hash Synchronization」，按下「Next」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add6.png "add6")<br>
 - 輸入您具有的 Azure AD Global administrator 的管理者帳號，按下「Next」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add7.png "add7")<br>
 - 點選「Add Directory」，選擇「Create new AD account」，輸入您具有 Enterprise admin 權限的帳號，按下「OK」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add8.png "add8")<br>
 - 成功後，可以看到您的樹系標示成功，按下「Next」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add9.png "add9")<br>
 - 因為此範例已經實作 Azure AD 自訂網域設定，在 Windows ADDS 樹系名稱一致的狀況下，按下「Next」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add10.png "add10")<br>
  > **Tips.如果您沒有實作自訂網域，請勾選 Continue without matching all UPN suffixes to verified domains 後繼續** <br>
 - 選擇「Sync selected domains and OUs」，只勾選「AVD」，按下「Next」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add11.png "add11")<br>
 - 按下「Next」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add12.png "add12")<br>
 - 按下「Next」，如果您想針對名稱、群組等篩選，您可以在此設定<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add13.png "add13")<br>
 - 按下「Next」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add14.png "add14")<br>
 - 選擇「Install」<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add15.png "add15")<br>
 - 完成<br>
  ![GITHUB](https://github.com/BrianHsing/Azure-Virtual-Desktop/blob/master/Lab2/add16.png "add16")<br>