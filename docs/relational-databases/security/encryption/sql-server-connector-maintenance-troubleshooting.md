---
title: SQL Server 커넥터 유지 관리 &amp; 문제 해결 | Microsoft 문서
ms.custom: ''
ms.date: 04/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a8f4b4a73139a698d481b65e1ebe93b524e2d863
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32973878"
---
# <a name="sql-server-connector-maintenance-amp-troubleshooting"></a>SQL Server 커넥터 유지 관리 &amp; 문제 해결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에 대한 추가 정보는 이 항목에서 제공됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에 대한 자세한 내용은 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md), [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md) 및 [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)을 참조하세요.  
  
  
##  <a name="AppendixA"></a> 1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에 대한 유지 관리 지침  
  
### <a name="key-rollover"></a>키 롤오버  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터는 “a-z”, “A-Z”, “0-9” 및 “-” 문자만 키 이름에 사용할 수 있으며, 키 이름은 26자로 제한됩니다.   
> Azure 주요 자격 증명 모음에서 동일한 키 이름의 여러 키 버전은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터와 함께 작동되지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용되는 Azure 주요 자격 증명 모음 키를 회전하려면 새 키 이름을 사용하는 새 키를 만들어야 합니다.  
  
 일반적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화에 대한 서버 비대칭 키는 1-2년마다 버전을 관리해야 합니다. 주요 자격 증명 모음에서는 키의 버전 관리가 허용되지만 버전 관리를 구현하기 위해 고객이 해당 기능을 사용하면 안 된다는 점에 유의해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에서는 주요 자격 증명 모음 키 버전의 변경 사항을 처리할 수 없습니다. 키 버전 관리를 구현하려면 고객은 주요 자격 증명 모음에서 새 키를 만든 다음 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 데이터 암호화 키를 다시 암호화해야 합니다.  
  
 TDE의 경우 이 작업을 수행하는 방법은 다음과 같습니다.  
  
-   **PowerShell:** 주요 자격 증명 모음에 새 비대칭 키(현재 TDE 비대칭 키와 다른 이름)를 만듭니다.  
  
    ```powershell  
    Add-AzureRmKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
-   **[!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 또는 sqlcmd.exe 사용:** 섹션 3, 3단계에 표시된 대로 다음 문을 사용합니다.  
  
     새 비대칭 키를 가져옵니다.  
  
    ```sql  
    USE master  
    CREATE ASYMMETRIC KEY [MASTER_KEY2]   
    FROM PROVIDER [EKM]   
    WITH PROVIDER_KEY_NAME = 'Key2',   
    CREATION_DISPOSITION = OPEN_EXISTING   
    GO  
    ```  
  
     TDE 지침 아래에 표시된 대로 새 비대칭 키와 연결할 새 로그인을 만듭니다.  
  
    ```sql  
    USE master  
    CREATE LOGIN TDE_Login2   
    FROM ASYMMETRIC KEY [MASTER_KEY2]  
    GO  
    ```  
  
     로그인에 매핑될 새 자격 증명을 만듭니다.  
  
    ```sql  
    CREATE CREDENTIAL Azure_EKM_TDE_cred2  
        WITH IDENTITY = 'ContosoDevKeyVault',   
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789=’   
    FOR CRYPTOGRAPHIC PROVIDER EKM;  
  
    ALTER LOGIN TDE_Login2  
    ADD CREDENTIAL Azure_EKM_TDE_cred2;  
    GO  
    ```  
  
     다시 암호화할 데이터베이스 암호화 키의 데이터베이스를 선택합니다.  
  
    ```sql  
    USE [database]  
    GO  
    ```  
  
     데이터베이스 암호화 키를 다시 암호화합니다.  
  
    ```sql  
    ALTER DATABASE ENCRYPTION KEY   
    ENCRYPTION BY SERVER ASYMMETRIC KEY [MASTER_KEY2];  
    GO  
    ```  
  
### <a name="upgrade-of-includessnoversionincludesssnoversion-mdmd-connector"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 업그레이드  

1.0.0.440 및 이전 버전은 대체되었으며 프로덕션 환경에서 더 이상 지원되지 않습니다. 버전 1.0.1.0 이상이 프로덕션 환경에서 지원됩니다. 다음 지침을 사용하여 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=45344)에서 제공하는 최신 버전으로 업그레이드하세요.

현재 1.0.1.0 이상 버전을 사용 중인 경우 다음 단계에 따라 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터의 최신 버전으로 업데이트하세요. 이 지침을 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작하지 않아도 됩니다.
 
1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Microsoft 다운로드 센터 [에서 최신 버전의](https://www.microsoft.com/download/details.aspx?id=45344)커넥터를 설치합니다. 설치 관리자 마법사에서 원래의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 DLL의 파일 경로와 다른 파일 경로에 새 DLL 파일을 저장합니다. 예를 들면 새 파일 경로는 다음과 같습니다. `C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll`
 
2. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에서 다음 TRANSACT-SQL 명령을 실행하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 새 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 가리키도록 합니다.

    ``` 
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll'
    GO  
    ```

현재 1.0.0.440 이전 버전을 사용 중인 경우 다음 단계에 따라 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터의 최신 버전으로 업데이트하세요.
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스를 중지합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 서비스를 중지합니다.  
  
3.  Windows의 프로그램 및 기능을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 제거합니다.  
  
     또는 DLL 파일이 들어 있는 폴더 이름을 바꿀 수 있습니다. 폴더의 기본 이름은 “[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for Microsoft Azure Key Vault”입니다.  
  
4.  Microsoft 다운로드 센터에서 최신 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 설치합니다.  
  
5.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스를 다시 시작합니다.  
  
6.  다음 문을 실행하여 EKM 공급자를 변경하고 최신 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 사용합니다. 파일 경로가 최신 버전을 다운로드한 위치를 가리키고 있는지 확인합니다. 원본 버전과 동일한 위치에 새 버전을 설치 중인 경우에는 이 단계를 건너뛸 수 있습니다. 
  
    ```sql  
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
7.  TDE를 사용하는 데이터베이스에 액세스할 수 있는지 확인합니다.  
  
8.  업데이트가 작동하는지 확인한 후, 3단계에서 제거하는 대신 이름을 변경하기로 선택한 경우 이전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 폴더를 삭제할 수 있습니다.  
  
### <a name="rolling-the-includessnoversionincludesssnoversion-mdmd-service-principal"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 사용자 롤링  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Azure Active Directory에서 만든 서비스 사용자를 자격 증명으로 사용하여 주요 자격 증명 모음에 액세스합니다.  서비스 사용자에게는 클라이언트 ID 및 인증 키가 있습니다.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 자격 증명은 **VaultName**, **클라이언트 ID**및 **인증 키**를 사용하여 설정됩니다.  **인증 키** 는 특정 기간(1년 또는 2년) 동안 유효합니다.   기간이 만료되기 전에 서비스 사용자에 대해 Azure AD에서 새 키를 생성해야 합니다.  그런 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 자격 증명을 변경해야 합니다.    [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 현재 세션에서 자격 증명에 대한 캐시를 유지 관리하므로 자격 증명이 변경되면 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 을(를) 다시 시작해야 합니다.  
  
### <a name="key-backup-and-recovery"></a>키 백업 및 복구  
주요 자격 증명 모음은 정기적으로 백업해야 합니다. 자격 증명 모음에 있는 비대칭 키를 분실한 경우 백업에서 복원할 수 있습니다. 키는 이전과 동일한 이름을 사용하여 복원되어야 하며, Restore PowerShell 명령으로 복원할 수 있습니다(아래 단계 참조).  
자격 증명 모음이 손실된 경우에는 자격 증명 모음을 다시 만들고 이전과 동일한 이름을 사용하여 자격 증명 모음에 비대칭 키를 복원해야 합니다. 자격 증명 모음 이름은 이전과 동일하거나, 달라질 수 있습니다. 또한 SQL Server 서비스 사용자에게 SQL Server 암호화 시나리오에 필요한 액세스 권한을 부여할 수 있도록 새 자격 증명 모음에 액세스 권한을 설정하고 새 자격 증명 모음 이름이 반영되도록 SQL Server 자격 증명을 조정해야 합니다.  
요약하면 다음 단계와 같습니다.  
  
* 자격 증명 모음 키를 백업합니다(Backup-AzureKeyVaultKey Powershell cmdlet 사용).  
* 자격 증명 모음이 실패하는 경우 동일한 지역*에서 새 자격 증명 모음을 만듭니다. 이 자격 증명 모음을 만드는 사용자는 SQL Server의 서비스 사용자 설정과 같은 기본 디렉터리에 있어야 합니다.  
* 새 자격 증명 모음에 키를 복원합니다(Restore-AzureKeyVaultKey Powershell cmdlet 사용 - 이전과 동일한 이름을 사용하여 키가 복원됨). 동일한 이름의 키가 이미 있는 경우 복원이 실패합니다.  
* 이 새 자격 증명 모음을 사용할 수 있도록 SQL Server 서비스 사용자에게 권한을 부여합니다.  
* 새 자격 증명 모음 이름이 반영되도록 데이터베이스 엔진에서 사용하는 SQL Server 자격 증명을 수정합니다(필요할 경우).  
  
키 백업은 동일한 지역 또는 국가(미국, 캐나다, 일본, 오스트레일리아, 인도, APAC, 유럽, 브라질, 중국, 미국 정부 또는 독일) 클라우드에 있는 경우 Azure 지역에서 복원할 수 있습니다.  
  
  
##  <a name="AppendixB"></a> 2. 질문과 대답  
### <a name="on-azure-key-vault"></a>Azure 주요 자격 증명 모음에서  
  
**Azure 주요 자격 증명 모음에서 키 작업은 어떻게 작동하나요?**  
 주요 자격 증명 모음에 있는 비대칭 키는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 키를 보호하는 데 사용됩니다. 비대칭 키의 공개 부분만 자격 증명 모음을 떠나고 비공개 부분은 자격 증명 모음에서 내보내지 않습니다. 비대칭 키를 사용하는 모든 암호화 작업은 Azure 주요 자격 증명 모음 서비스 내에서 수행되며, 서비스의 보안에 의해 보호됩니다.  
  
 **키 URI는 무엇인가요?**  
 Azure 주요 자격 증명 모음의 모든 키에는 응용 프로그램에서 키를 참조하는 데 사용할 수 있는 URI(Uniform Resource Identifier)가 있습니다. 현재 버전을 가져오려면 `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` 형식을 사용하고, 특정 버전을 가져오려면 `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` 형식을 사용합니다.  
  
### <a name="on-configuring-includessnoversionincludesssnoversion-mdmd"></a>구성에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

**SQL Server 커넥터에서 액세스해야 하는 끝점은 무엇인가요?** 커넥터는 허용 목록에 포함되어야 하는 두 개의 끝점과 통신합니다. Https의 경우 이러한 다른 서비스에 대한 아웃바운드 통신에 필요한 유일한 포트는 443입니다.
-  login.microsoftonline.com/*:443
-  *.vault.azure.net/*:443
  
**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 각 구성 단계에 대해 필요한 최소 권한 수준은 무엇인가요?**  
 sysadmin 고정 서버 역할이 있는 멤버로 구성 단계를 모두 수행할 수는 있지만 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 사용할 권한을 최소화하는 것이 권장됩니다. 다음 목록에서는 각 작업에 대한 최소 권한 수준을 정의합니다.  
  
-   암호화 공급자를 만들려면 `CONTROL SERVER` sysadmin **고정 서버 역할에** 권한 또는 멤버 자격이 있어야 합니다.  
  
-   구성 옵션을 변경하고 `RECONFIGURE` 문을 실행하려면 `ALTER SETTINGS` 서버 수준 권한이 있어야 합니다. sysadmin 및 `ALTER SETTINGS` serveradmin **고정 서버 역할은** 권한을 암시적으로 보유하고 있습니다.  
  
-   자격 증명을 만들려면 `ALTER ANY CREDENTIAL` 권한이 필요합니다.  
  
-   로그인에 자격 증명을 추가하려면 `ALTER ANY LOGIN` 권한이 필요합니다.  
  
-   비대칭 키를 만들려면 `CREATE ASYMMETRIC KEY` 권한이 필요합니다.  

**[!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 커넥터에 대해 만든 서비스 주체와 동일한 구독과 Active Directory에서 내 키 자격 증명 모음을 만들려면 내 기본 Active Directory를 어떻게 변경하나요?**

![aad-change-default-directory-helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. Azure 클래식 포털[https://manage.windowsazure.com](https://manage.windowsazure.com)로 이동합니다.  
2. 왼쪽 메뉴에서 아래로 스크롤하여 **설정**을 선택합니다.
3. 현재 사용 중인 Azure 구독을 선택하고 화면 맨 아래에 있는 명령에서 **디렉터리 편집** 을 클릭합니다.
4. 팝업 창에서 **디렉터리** 드롭다운을 사용하여 원하는 Active Directory를 선택합니다. 이 디렉터리가 기본 디렉터리로 설정됩니다.
5. 본인이 새로 선택한 Active Directory의 전역 관리자인지 확인합니다. 전역 관리자가 아닌 경우에는 디렉터리를 전환했으므로 관리 권한이 없어졌을 수도 있습니다.
6. 팝업 창이 닫히고 구독이 표시되지 않으면 새로 업데이트된 Active Directory를 사용하는 구독을 확인하기 위해 화면 오른쪽 위 메뉴에 있는 **구독** 필터에서 **디렉터리로 필터링** 필터를 업데이트해야 할 수도 있습니다.

    > [!NOTE] 
    > Azure 구독에 기본 디렉터리를 실제로 변경할 수 있는 권한이 없을 수 있습니다. 이 경우에는 기본 디렉터리에 AAD 서비스 주체를 만들어 나중에 사용되는 Azure Key Vault와 동일한 디렉터리에 있도록 합니다.

Active Directory에 대한 자세한 내용을 보려면 [Azure Active Directory와 관련된 Azure 구독](https://azure.microsoft.com/documentation/articles/active-directory-how-subscriptions-associated-directory/)을 참조하세요.
  
##  <a name="AppendixC"></a> 3. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에 대한 오류 코드 설명  
 **공급자 오류 코드**  
  
오류 코드  |기호  |Description    
---------|---------|---------  
0 | scp_err_Success | 작업이 성공했습니다.    
1 | scp_err_Failure | 작업이 실패했습니다.    
2 | scp_err_InsufficientBuffer | 이 오류는 엔진에 버퍼에 대해 더 많은 메모리를 할당하라고 알립니다.    
3 | scp_err_NotSupported | 이 작업은 지원되지 않습니다. 예를 들어, 지정된 키 유형 또는 알고리즘을 EKM 공급자가 지원하지 않습니다.    
4 | scp_err_NotFound | EKM 공급자가 지정된 키 또는 알고리즘을 찾을 수 없습니다.    
5 | scp_err_AuthFailure | EKM 공급자가 인증에 실패했습니다.    
6 | scp_err_InvalidArgument | 제공된 인수가 잘못되었습니다.    
7 | scp_err_ProviderError | EKM 공급자에 지정되지 않은 오류가 있으며 SQL 엔진에서 발견했습니다.    
2049 | scp_err_KeyNameDoesNotFitThumbprint | 키 이름이 너무 길어 SQL 엔진의 지문에 맞지 않습니다. 키 이름은 26자를 초과할 수 없습니다.    
2050 | scp_err_PasswordTooShort | AAD 클라이언트 ID 및 암호의 연결인 암호 문자열이 32자 미만입니다.    
2051 | scp_err_OutOfMemory | SQL 엔진에 메모리가 부족하며 EKM 공급자에 대한 메모리를 할당하지 못했습니다.    
2052 | scp_err_ConvertKeyNameToThumbprint | 키 이름을 지문으로 변환하지 못했습니다.    
2053 | scp_err_ConvertThumbprintToKeyName|  지문을 키 이름으로 변환하지 못했습니다.    
3000 | ErrorSuccess | AKV 작업이 성공했습니다.    
3001 | ErrorUnknown | 지정되지 않은 오류가 발생했으며 AKV 작업이 실패했습니다.    
3002 | ErrorHttpCreateHttpClientOutOfMemory | 메모리 부족으로 인해 AKV 작업에 대한 HttpClient를 만들 수 없습니다.    
3003 | ErrorHttpOpenSession | 네트워크 오류로 인해 Http 세션을 열 수 없습니다.    
3004 | ErrorHttpConnectSession | 네트워크 오류로 인해 Http 세션을 연결할 수 없습니다.    
3005 | ErrorHttpAttemptConnect | 네트워크 오류로 인해 연결을 시도할 수 없습니다.    
3006 | ErrorHttpOpenRequest | 네트워크 오류로 인해 요청을 열 수 없습니다.    
3007 | ErrorHttpAddRequestHeader | 요청 헤더를 추가할 수 없습니다.    
3008 | ErrorHttpSendRequest | 네트워크 오류로 인해 요청을 보낼 수 없습니다.    
3009 | ErrorHttpGetResponseCode | 네트워크 오류로 인해 응답 코드를 가져올 수 없습니다.    
3010 | ErrorHttpResponseCodeUnauthorized | 서버는 요청에 대해 401을 응답했습니다.    
3011 | ErrorHttpResponseCodeThrottled | 서버에서 요청을 제한했습니다.    
3012 | ErrorHttpResponseCodeClientError | 커넥터에서 보낸 요청이 잘못되었습니다. 이 문제는 일반적으로 키 이름이 잘못되었거나 잘못된 문자가 포함되었음을 의미합니다.
3013 | ErrorHttpResponseCodeServerError | 서버에서 응답 코드 500 ~ 600을 응답했습니다.    
3014 | ErrorHttpQueryHeader | 응답 헤더에 대해 쿼리할 수 없습니다.    
3015 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader | 메모리가 부족하여 응답 헤더를 복사할 수 없습니다.    
3016 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer | 버퍼를 재할당할 때 메모리가 부족하여 응답 헤더를 쿼리할 수 없습니다.    
3017 | ErrorHttpQueryHeaderNotFound | 응답에서 쿼리 헤더를 찾을 수 없습니다.    
3018 | ErrorHttpQueryHeaderUpdateBufferLength | 응답 헤더를 쿼리할 때에 버퍼 길이를 업데이트할 수 없습니다.    
3019 | ErrorHttpReadData | 네트워크 오류로 인해 응답 데이터를 읽을 수 없습니다. 
3076 | ErrorHttpResourceNotFound | 키 이름을 알 수 없어 서버에서 404로 응답했습니다. 사용자 자격 증명 모음에 키 이름이 있는지 확인하세요.
3077 | ErrorHttpOperationForbidden | 사용자에게 작업을 수행할 적절한 권한이 없어 403으로 응답했습니다. 지정된 작업에 대한 권한이 있는지 확인하세요. 최소한 커넥터가 제대로 작동하려면 'get, list, wrapKey, unwrapKey' 권한이 필요합니다.   
  
이 테이블에 오류 코드가 표시되지 않는 경우, 다음과 같은 다른 이유로 오류가 발생할 수 있습니다.   
  
-   인터넷 액세스 권한이 없으며 Azure 주요 자격 증명 모음에 액세스할 수 없습니다. 인터넷 연결을 확인하세요.  
  
-   Azure 주요 자격 증명 모음 서비스가 종료될 수 있습니다. 나중에 다시 시도하세요.  
  
-   Azure 주요 자격 증명 모음 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 비대칭 키를 삭제했을 수 있습니다. 키를 복원하세요.  
  
-   "라이브러리를 로드할 수 없습니다." 오류가 표시되는 경우 실행 중인 SQL Server 버전에 적절한 재배포 가능한 Visual Studio C++의 최신 버전이 설치되어 있는지 확인하세요. 다음 표에서는 Microsoft 다운로드 센터에서 설치할 버전을 지정합니다.   
  
SQL Server 버전  |재배포 가능 설치 링크    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Visual Studio 2013용 Visual C++ 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual Studio 2015용 Visual C++ 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=48145)    
  
  
## <a name="additional-references"></a>추가 참조  
 확장 가능 키 관리 추가 정보:  
  
-   [확장 가능 키 관리 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 EKM을 지원하는 SQL 암호화:  
  
-   [EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
-   [백업 암호화](../../../relational-databases/backup-restore/backup-encryption.md)  
  
-   [암호화된 백업 만들기](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 관련 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령:  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Azure 주요 자격 증명 모음 설명서:  
  
-   [Azure 키 자격 증명 모음이란?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/)  
  
-   [Azure 키 자격 증명 모음 시작](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)  
  
-   PowerShell [Azure 주요 자격 증명 모음 Cmdlet](https://msdn.microsoft.com/library/dn868052.aspx) 참조  
  
## <a name="see-also"></a>참고 항목  
 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)   
 [EKM provider enabled 서버 구성 옵션](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)  
  
  
