---
title: SQL Server 커넥터 유지 관리 및 문제 해결
description: SQL Server 커넥터의 유지 관리 지침 및 일반적인 문제 해결 단계를 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 10/08/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 4c8a74d33e75ab19b283f3b9d1bfdaf47dc69240
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869261"
---
# <a name="sql-server-connector-maintenance--troubleshooting"></a>SQL Server 커넥터, 부록

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에 대한 추가 정보는 이 항목에서 제공됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에 대한 자세한 내용은 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md), [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md) 및 [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)을 참조하세요.  
  
##  <a name="a-maintenance-instructions-for-ssnoversion-connector"></a><a name="AppendixA"></a> 1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에 대한 유지 관리 지침  
  
### <a name="key-rollover"></a>키 롤오버  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터는 “a-z”, “A-Z”, “0-9” 및 “-” 문자만 키 이름에 사용할 수 있으며, 키 이름은 26자로 제한됩니다.
> Azure 주요 자격 증명 모음에서 동일한 키 이름의 여러 키 버전은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터와 함께 작동되지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용되는 Azure Key Vault 키를 전환하려면 새 키 이름을 사용하는 새 키를 만들어야 합니다.  
  
 일반적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화에 사용되는 서버 비대칭 키의 경우 1~2년마다 버전을 관리해야 합니다. 주요 자격 증명 모음에서는 키의 버전 관리가 허용되지만 버전 관리를 구현하기 위해 고객이 해당 기능을 사용하면 안 된다는 점에 유의해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에서는 주요 자격 증명 모음 키 버전의 변경 사항을 처리할 수 없습니다. 키 버전 관리를 구현하려면 Key Vault에 새 키를 만든 다음, [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 데이터 암호화 키를 다시 암호화합니다.  
  
 TDE의 경우 이 작업을 수행하는 방법은 다음과 같습니다.  
  
- **PowerShell:** 주요 자격 증명 모음에 새 비대칭 키(현재 TDE 비대칭 키와 다른 이름)를 만듭니다.  
  
    ```powershell  
    Add-AzKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
- **[!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 또는 sqlcmd.exe 사용:** 섹션 3, 3단계에 표시된 대로 다음 문을 사용합니다.  
  
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
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789='
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
  
### <a name="upgrade-of-ssnoversion-connector"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 업그레이드  

1\.0.0.440 및 이전 버전은 대체되었으며 프로덕션 환경에서 더 이상 지원되지 않습니다. 버전 1.0.1.0 이상이 프로덕션 환경에서 지원됩니다. 다음 지침을 사용하여 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=45344)에서 제공하는 최신 버전으로 업그레이드하세요.

### <a name="upgrade"></a>업그레이드

1. SQL Server 구성 관리자를 사용하여 SQL Server 서비스를 중지합니다.
1. 제어판\프로그램\프로그램 및 기능을 사용하여 이전 버전을 제거합니다.
    1. 애플리케이션 이름: Microsoft Azure Key Vault용 SQL Server 커넥터
    1. 버전: 15.0.300.96(또는 이전 버전)
    1. DLL 파일 날짜: 2018-01-30 오후 3:00(또는 이전 버전)
1. 새로운 Microsoft Azure 주요 자격 증명 모음용 SQL Server 커넥터를 설치(업그레이드)합니다.
    1. 버전: 15.0.2000.367
    1. DLL 파일 날짜: 2020-09-11 ‏‎오전 5:17
1. SQL Server 서비스를 시작합니다.
1. 암호화된 DB에 액세스할 수 있는지 테스트합니다.

### <a name="rollback"></a>롤백

1. SQL Server 구성 관리자를 사용하여 SQL Server 서비스를 중지합니다.

1. 제어판\프로그램\프로그램 및 기능을 사용하여 새 버전을 제거합니다.
    1. 애플리케이션 이름: Microsoft Azure Key Vault용 SQL Server 커넥터
    1. 버전: 15.0.2000.367
    1. DLL 파일 날짜: 2020-09-11 ‏‎오전 5:17

1. 이전 버전의 Microsoft Azure 주요 자격 증명 모음용 SQL Server 커넥터를 설치합니다.
    1. 버전: 15.0.300.96
    1. DLL 파일 날짜: 2018-01-30 오후 3:00
1. SQL Server 서비스를 시작합니다.

1. TDE를 사용하는 데이터베이스에 액세스할 수 있는지 확인합니다.  
  
1. 업데이트가 작동하는지 확인한 후, 3단계에서 제거하는 대신 이름을 변경하기로 선택한 경우 이전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터 폴더를 삭제할 수 있습니다.

### <a name="older-versions-of-the-sql-server-connector"></a>이전 버전의 SQL Server 커넥터
  
이전 버전의 SQL Server 커넥터 딥 링크

- 현재: [1.0.5.0(버전 15.0.2000.367) – 파일 날짜 2020년 9월 11일](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/1033_15.0.2000.367/SQLServerConnectorforMicrosoftAzureKeyVault.msi)
- [1.0.5.0(버전 15.0.300.96) – 파일 날짜 2018년 1월 30일](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/ENU/SQLServerConnectorforMicrosoftAzureKeyVault.msi)
- [1.0.4.0(버전 13.0.811.168)](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/SQLServerConnectorforMicrosoftAzureKeyVault.msi)

### <a name="rolling-the-ssnoversion-service-principal"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 사용자 롤링

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Azure Active Directory에서 만든 서비스 사용자를 자격 증명으로 사용하여 주요 자격 증명 모음에 액세스합니다. 서비스 사용자에게는 클라이언트 ID 및 인증 키가 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 자격 증명은 **VaultName**, **클라이언트 ID**및 **인증 키**를 사용하여 설정됩니다. **인증 키**는 특정 기간(1년 또는 2년) 동안 유효합니다. 기간이 만료되기 전에 서비스 사용자에 대해 Azure AD에서 새 키를 생성해야 합니다. 그런 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 자격 증명을 변경해야 합니다. [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 현재 세션에서 자격 증명에 대한 캐시를 유지 관리하므로 자격 증명이 변경되면 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 을(를) 다시 시작해야 합니다.  
  
### <a name="key-backup-and-recovery"></a>키 백업 및 복구

주요 자격 증명 모음은 정기적으로 백업해야 합니다. 자격 증명 모음에 있는 비대칭 키를 분실한 경우 백업에서 복원할 수 있습니다. 키는 이전과 동일한 이름을 사용하여 복원되어야 하며, Restore PowerShell 명령으로 복원할 수 있습니다(아래 단계 참조).  
자격 증명 모음이 손실된 경우에는 자격 증명 모음을 다시 만들고 이전과 동일한 이름을 사용하여 자격 증명 모음에 비대칭 키를 복원해야 합니다. 자격 증명 모음 이름은 이전과 동일하거나, 달라질 수 있습니다. 새 자격 증명 모음에 액세스 권한을 설정하여 SQL Server 서비스 주체에게 SQL Server 암호화 시나리오에 필요한 액세스 권한을 부여한 다음, 새 자격 증명 모음 이름을 반영하여 SQL Server 자격 증명을 조정합니다.

요약하면 다음 단계와 같습니다.  
  
- 자격 증명 모음 키를 백업합니다(Backup-AzureKeyVaultKey PowerShell cmdlet 사용).  
- 자격 증명 모음 오류가 발생할 경우 동일한 지역에 새 자격 증명 모음을 만듭니다. 자격 증명 모음을 만드는 사용자는 SQL Server에 설정된 서비스 주체와 동일한 기본 디렉터리에 있어야 합니다.  
- Restore-AzureKeyVaultKey PowerShell cmdlet을 사용하여 키를 새 자격 증명 모음에 복원합니다. 이전과 동일한 이름으로 키가 복원됩니다. 동일한 이름의 키가 이미 있으면 복원에 실패합니다.  
- 이 새 자격 증명 모음을 사용할 수 있도록 SQL Server 서비스 사용자에게 권한을 부여합니다.
- 새 자격 증명 모음 이름이 반영되도록 데이터베이스 엔진에서 사용하는 SQL Server 자격 증명을 수정합니다(필요할 경우).  
  
키 백업은 동일한 지리적 지역 또는 미국, 캐나다, 일본, 오스트레일리아, 인도, APAC, 유럽, 브라질, 중국, 미국 정부, 독일 등의 국가별 클라우드에 있다면 다양한 Azure 지역에서 복원할 수 있습니다.  
  
##  <a name="b-frequently-asked-questions"></a><a name="AppendixB"></a> 2. 질문과 대답

### <a name="on-azure-key-vault"></a>Azure 주요 자격 증명 모음에서
  
**Azure 주요 자격 증명 모음에서 키 작업은 어떻게 작동하나요?**  
 주요 자격 증명 모음에 있는 비대칭 키는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 키를 보호하는 데 사용됩니다. 비대칭 키의 퍼블릭 부분만 자격 증명 모음을 떠나고 프라이빗 부분은 자격 증명 모음에서 내보내지 않습니다. 비대칭 키를 사용하는 모든 암호화 작업은 Azure Key Vault 서비스 내에서 수행되며, 서비스 보안에 의해 보호됩니다.  
  
 **키 URI는 무엇인가요?**  
 Azure 주요 자격 증명 모음의 모든 키에는 애플리케이션에서 키를 참조하는 데 사용할 수 있는 URI(Uniform Resource Identifier)가 있습니다. 현재 버전을 가져오려면 `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` 형식을 사용하고, 특정 버전을 가져오려면 `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` 형식을 사용합니다.  
  
### <a name="on-configuring-ssnoversion"></a>구성에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

**SQL Server 커넥터에서 액세스해야 하는 엔드포인트는 무엇인가요?**
커넥터는 허용해야 하는 두 개의 엔드포인트와 통신합니다. Https의 경우 이러한 다른 서비스에 대한 아웃바운드 통신에 필요한 유일한 포트는 443입니다.

- login.microsoftonline.com/*:443
- *.vault.azure.net/* :443

**HTTP(S) 프록시 서버를 통해 Azure Key Vault에 연결하려면 어떻게 할까요?**
커넥터는 Internet Explorer의 프록시 구성 설정을 사용합니다. [그룹 정책](/archive/blogs/askie/how-to-configure-proxy-settings-for-ie10-and-ie11-as-iem-is-not-available) 또는 레지스트리를 통해 설정을 제어할 수 있지만, 시스템 수준 설정이 아니라 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 서비스 계정을 대상으로 해야 합니다. 데이터베이스 관리자가 Internet Explorer에서 보거나 편집하는 설정은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 엔진이 아니라 데이터베이스 관리자 계정에만 영향을 줍니다. 서비스 계정을 사용하여 대화형으로 서버에 로그온하는 것은 권장되지 않으며 여러 보안 환경에서 차단됩니다. 구성된 프록시 설정을 변경하는 경우, 커넥터가 키 자격 증명 모음에 처음 연결할 때 설정이 캐시되었기 때문에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작해야 변경 내용을 적용할 수 있습니다.

**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 각 구성 단계에 대해 필요한 최소 권한 수준은 무엇인가요?**  
 sysadmin 고정 서버 역할이 있는 멤버로 구성 단계를 모두 수행할 수는 있지만 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 사용할 권한을 최소화하는 것이 권장됩니다. 다음 목록에서는 각 작업에 대한 최소 권한 수준을 정의합니다.  
  
- 암호화 공급자를 만들려면 `CONTROL SERVER` sysadmin **고정 서버 역할에** 권한 또는 멤버 자격이 있어야 합니다.  
  
- 구성 옵션을 변경하고 `RECONFIGURE` 문을 실행하려면 `ALTER SETTINGS` 서버 수준 권한이 있어야 합니다. sysadmin 및 `ALTER SETTINGS` serveradmin **고정 서버 역할은** 권한을 암시적으로 보유하고 있습니다.  
  
- 자격 증명을 만들려면 `ALTER ANY CREDENTIAL` 권한이 필요합니다.  
  
- 로그인에 자격 증명을 추가하려면 `ALTER ANY LOGIN` 권한이 필요합니다.  
  
- 비대칭 키를 만들려면 `CREATE ASYMMETRIC KEY` 권한이 필요합니다.  

**[!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] 커넥터에 대해 만든 서비스 주체와 동일한 구독과 Active Directory에서 내 키 자격 증명 모음을 만들려면 내 기본 Active Directory를 어떻게 변경하나요?**

![aad change default directory helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. Azure 클래식 포털[https://manage.windowsazure.com](https://manage.windowsazure.com)로 이동합니다.  
2. 왼쪽 메뉴에서 **설정**을 선택합니다.
3. 현재 사용 중인 Azure 구독을 선택하고 화면 맨 아래에 있는 명령에서 **디렉터리 편집** 을 클릭합니다.
4. 팝업 창에서 **디렉터리** 드롭다운을 사용하여 원하는 Active Directory를 선택합니다. 이 디렉터리가 기본 디렉터리로 설정됩니다.
5. 본인이 새로 선택한 Active Directory의 전역 관리자인지 확인합니다. 전역 관리자가 아닌 경우 디렉터리를 전환했으므로 관리 권한이 없어졌을 수도 있습니다.
6. 팝업 창이 닫히고 구독이 표시되지 않으면 새로 업데이트된 Active Directory를 사용하는 구독을 확인하기 위해 화면 오른쪽 위 메뉴에 있는 **구독** 필터에서 **디렉터리로 필터링** 필터를 업데이트해야 할 수도 있습니다.

    > [!NOTE] 
    > Azure 구독에 기본 디렉터리를 실제로 변경할 수 있는 권한이 없을 수 있습니다. 이 경우에는 기본 디렉터리에 AAD 서비스 주체를 만들어 나중에 사용되는 Azure Key Vault와 동일한 디렉터리에 있도록 합니다.

Active Directory에 대한 자세한 내용을 보려면 [Azure Active Directory와 관련된 Azure 구독](/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory)을 참조하세요.
  
##  <a name="c-error-code-explanations-for-ssnoversion-connector"></a><a name="AppendixC"></a> 3. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터에 대한 오류 코드 설명

**공급자 오류 코드**  
  
오류 코드  |기호  |설명
---------|---------|---------  
0 | scp_err_Success | 작업이 성공했습니다.
1 | scp_err_Failure | 작업이 실패했습니다.
2 | scp_err_InsufficientBuffer | 이 오류는 엔진에 버퍼에 대해 더 많은 메모리를 할당하라고 알립니다.
3 | scp_err_NotSupported | 이 작업은 지원되지 않습니다. 예를 들어 지정된 키 유형 또는 알고리즘을 EKM 공급자가 지원하지 않습니다.
4 | scp_err_NotFound | EKM 공급자가 지정된 키 또는 알고리즘을 찾을 수 없습니다.
5 | scp_err_AuthFailure | EKM 공급자가 인증에 실패했습니다.
6 | scp_err_InvalidArgument | 제공된 인수가 잘못되었습니다.
7 | scp_err_ProviderError | EKM 공급자에 지정되지 않은 오류가 있으며 SQL 엔진에서 발견했습니다.
401 | acquireToken | 서버는 요청에 대해 401을 응답했습니다. 클라이언트 ID와 비밀이 올바르고, 자격 증명 문자열이 AAD 클라이언트 ID와 비밀을 하이픈 없이 연결한 값인지 확인합니다.
404 | getKeyByName | 키 이름을 알 수 없어 서버에서 404로 응답했습니다. 사용자 자격 증명 모음에 키 이름이 있는지 확인하세요.
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
3077 | ErrorHttpOperationForbidden | 사용자가 작업을 수행할 적절한 권한이 없어 서버가 403으로 응답했습니다. 지정된 작업에 대한 권한이 있는지 확인하세요. 최소한 커넥터가 제대로 작동하려면 'get, list, wrapKey, unwrapKey' 권한이 필요합니다.
3100 | ErrorHttpCreateHttpClientOutOfMemory               | 메모리 부족으로 인해 AKV 작업에 대한 HttpClient를 만들 수 없습니다.
3101 | ErrorHttpOpenSession                               | 네트워크 오류로 인해 Http 세션을 열 수 없습니다.
3102 | ErrorHttpConnectSession                            | 네트워크 오류로 인해 Http 세션을 연결할 수 없습니다.
3103 | ErrorHttpAttemptConnect                            | 네트워크 오류로 인해 연결을 시도할 수 없습니다.
3104 | ErrorHttpOpenRequest                               | 네트워크 오류로 인해 요청을 열 수 없습니다.
3105 | ErrorHttpAddRequestHeader                          | 요청 헤더를 추가할 수 없습니다.
3106 | ErrorHttpSendRequest                               | 네트워크 오류로 인해 요청을 보낼 수 없습니다.
3107 | ErrorHttpGetResponseCode                           | 네트워크 오류로 인해 응답 코드를 가져올 수 없습니다.
3108 | ErrorHttpResponseCodeUnauthorized                  | 서버는 요청에 대해 401을 응답했습니다. 클라이언트 ID와 비밀이 올바르고, 자격 증명 문자열이 AAD 클라이언트 ID와 비밀을 하이픈 없이 연결한 값인지 확인합니다.
3109 | ErrorHttpResponseCodeThrottled                     | 서버에서 요청을 제한했습니다.
3110 | ErrorHttpResponseCodeClientError                    | 요청이 잘못되었습니다. 이 문제는 일반적으로 키 이름이 잘못되었거나 잘못된 문자가 포함되었음을 의미합니다.
3111 | ErrorHttpResponseCodeServerError                   | 서버에서 응답 코드 500 ~ 600을 응답했습니다.
3112 | ErrorHttpResourceNotFound                          | 키 이름을 알 수 없어 서버에서 404로 응답했습니다. 사용자 자격 증명 모음에 키 이름이 있는지 확인하세요.
3113 | ErrorHttpOperationForbidden                         | 사용자가 작업을 수행할 적절한 권한이 없어 서버가 403으로 응답했습니다. 지정된 작업에 대한 권한이 있는지 확인하세요. 최소한 'get, wrapKey, unwrapKey' 권한이 필요합니다.
3114 | ErrorHttpQueryHeader                               | 응답 헤더에 대해 쿼리할 수 없습니다.
3115 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader          | 메모리가 부족하여 응답 헤더를 복사할 수 없습니다.
3116 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer       | 버퍼를 재할당할 때 메모리가 부족하여 응답 헤더를 쿼리할 수 없습니다.
3117 | ErrorHttpQueryHeaderNotFound                       | 응답에서 쿼리 헤더를 찾을 수 없습니다.
3118 | ErrorHttpQueryHeaderUpdateBufferLength             | 응답 헤더를 쿼리할 때에 버퍼 길이를 업데이트할 수 없습니다.
3119 | ErrorHttpReadData                                  | 네트워크 오류로 인해 응답 데이터를 읽을 수 없습니다.
3120 | ErrorHttpGetResponseOutOfMemoryCreateTempBuffer    | 메모리 부족으로 인해 임시 버퍼를 만들 때 응답 본문을 가져올 수 없습니다.
3121 | ErrorHttpGetResponseOutOfMemoryGetResultString     | 메모리 부족으로 인해 결과 문자열을 가져올 때 응답 본문을 가져올 수 없습니다.
3122 | ErrorHttpGetResponseOutOfMemoryAppendResponse      | 메모리 부족으로 인해 응답을 추가할 때 응답 본문을 가져올 수 없습니다.
3200 | ErrorGetAADValuesOutOfMemoryConcatPath | 메모리 부족으로 인해 경로를 연결할 때 Azure Active Directory 챌린지 헤더 값을 가져올 수 없습니다.
3201 | ErrorGetAADDomainUrlStartPosition | 잘못된 형식의 응답 챌린지 헤더에서 Azure Active Directory 도메인 URL의 시작 위치를 찾을 수 없습니다.
3202 | ErrorGetAADDomainUrlStopPosition | 잘못된 형식의 응답 챌린지 헤더에서 Azure Active Directory 도메인 URL의 끝 위치를 찾을 수 없습니다.
3203 | ErrorGetAADDomainUrlMalformatted | Azure Active Directory 응답 챌린지 헤더가 잘못된 형식이고 AAD 도메인 URL을 포함하지 않습니다.
3204 | ErrorGetAADDomainUrlOutOfMemoryAlloc | Azure Active Directory 도메인 URL에 대한 버퍼를 할당할 때 메모리가 부족합니다.
3205 | ErrorGetAADTenantIdOutOfMemoryAlloc | Azure Active Directory 테넌트 ID에 대한 버퍼를 할당할 때 메모리가 부족합니다.
3206 | ErrorGetAKVResourceUrlStartPosition | 잘못된 형식의 응답 챌린지 헤더에서 Azure Key Vault 리소스 URL의 시작 위치를 찾을 수 없습니다.
3207 | ErrorGetAKVResourceUrlStopPosition | 잘못된 형식의 응답 챌린지 헤더에서 Azure Key Vault 리소스 URL의 끝 위치를 찾을 수 없습니다.
3208 | ErrorGetAKVResourceUrlOutOfMemoryAlloc | Azure Key Vault 리소스 URL에 대한 버퍼를 할당할 때 메모리가 부족합니다.
3300 | ErrorGetTokenOutOfMemoryConcatPath | 메모리 부족으로 인해 요청 경로를 연결할 때 토큰을 가져올 수 없습니다.
3301 | ErrorGetTokenOutOfMemoryConcatBody | 메모리 부족으로 인해 응답 본문을 연결할 때 토큰을 가져올 수 없습니다.
3302 | ErrorGetTokenOutOfMemoryConvertResponseString | 메모리 부족으로 인해 응답 문자열을 변환할 때 토큰을 가져올 수 없습니다.
3303 | ErrorGetTokenBadCredentials | 잘못된 자격 증명으로 인해 토큰을 가져올 수 없습니다. 자격 증명 문자열 또는 인증서가 유효한지 확인합니다.
3304 | ErrorGetTokenFailedToGetToken | 자격 증명이 올바르지만 여전히 작업에서 올바른 토큰을 가져오지 못했습니다.
3305 | ErrorGetTokenRejected | 토큰이 올바르지만 서버에서 거부되었습니다.
3306 | ErrorGetTokenNotFound | 응답에서 토큰을 찾을 수 없습니다.
3307 | ErrorGetTokenJsonParser | 서버의 JSON 응답을 구문 분석할 수 없습니다.
3308 | ErrorGetTokenExtractToken | JSON 응답에서 토큰을 추출할 수 없습니다.
3400 | ErrorGetKeyByNameOutOfMemoryConvertResponseString | 메모리 부족으로 인해 응답 문자열을 변환할 때 이름을 기준으로 키를 가져올 수 없습니다.
3401 | ErrorGetKeyByNameOutOfMemoryConcatPath | 메모리 부족으로 인해 경로를 연결할 때 이름을 기준으로 키를 가져올 수 없습니다.
3402 | ErrorGetKeyByNameOutOfMemoryConcatHeader | 메모리 부족으로 인해 헤더를 연결할 때 이름을 기준으로 키를 가져올 수 없습니다.
3403 | ErrorGetKeyByNameNoResponse | 서버로부터 응답이 없기 때문에 이름을 기준으로 키를 가져올 수 없습니다.
3404 | ErrorGetKeyByNameJsonParser | JSON 응답을 구문 분석하지 못해 이름을 기준으로 키를 가져올 수 없습니다.
3405 | ErrorGetKeyByNameExtractKeyNode | 응답에서 키 노드를 추출하지 못해 이름을 기준으로 키를 가져올 수 없습니다.
3406 | ErrorGetKeyByNameExtractKeyId | 응답에서 키 ID를 추출하지 못해 이름을 기준으로 키를 가져올 수 없습니다.
3407 | ErrorGetKeyByNameExtractKeyType | 응답에서 키 유형을 추출하지 못해 이름을 기준으로 키를 가져올 수 없습니다.
3408 | ErrorGetKeyByNameExtractKeyN | 응답에서 키 N을 추출하지 못해 이름을 기준으로 키를 가져올 수 없습니다.
3409 | ErrorGetKeyByNameBase64DecodeN | N을 Base64 디코딩하지 못해 이름을 기준으로 키를 가져올 수 없습니다.
3410 | ErrorGetKeyByNameExtractKeyE | 응답에서 키 E를 추출하지 못해 이름을 기준으로 키를 가져올 수 없습니다.
3411 | ErrorGetKeyByNameBase64DecodeE | E를 Base64 디코딩하지 못해 이름을 기준으로 키를 가져올 수 없습니다.
3412 | ErrorGetKeyByNameExtractKeyUri | 응답에서 키 URI를 추출할 수 없습니다.
3500 | ErrorBackupKeyOutOfMemoryConvertResponseString | 메모리 부족으로 인해 응답 문자열을 변환할 때 키를 백업할 수 없습니다.
3501 | ErrorBackupKeyOutOfMemoryConcatPath | 메모리 부족으로 인해 경로를 연결할 때 키를 백업할 수 없습니다.
3502 | ErrorBackupKeyOutOfMemoryConcatHeader | 메모리 부족으로 인해 요청 헤더를 연결할 때 키를 백업할 수 없습니다.
3503 | ErrorBackupKeyNoResponse | 서버로부터 응답이 없기 때문에 키를 백업할 수 없습니다.
3504 | ErrorBackupKeyJsonParser | JSON 응답을 구문 분석하지 못해 키를 백업할 수 없습니다.
3505 | ErrorBackupKeyExtractValue | JSON 응답에서 값을 추출하지 못해 키를 백업할 수 없습니다.
3506 | ErrorBackupKeyBase64DecodeValue | 값 필드를 Base64 디코딩하지 못해 키를 백업할 수 없습니다.
3600 | ErrorWrapKeyOutOfMemoryConvertResponseString | 메모리 부족으로 인해 응답 문자열을 변환할 때 키를 래핑할 수 없습니다.
3601 | ErrorWrapKeyOutOfMemoryConcatPath | 메모리 부족으로 인해 경로를 연결할 때 키를 래핑할 수 없습니다.
3602 | ErrorWrapKeyOutOfMemoryConcatHeader | 메모리 부족으로 인해 헤더를 연결할 때 키를 래핑할 수 없습니다.
3603 | ErrorWrapKeyOutOfMemoryConcatBody | 메모리 부족으로 인해 본문을 연결할 때 키를 래핑할 수 없습니다.
3604 | ErrorWrapKeyOutOfMemoryConvertEncodedBody | 메모리 부족으로 인해 인코딩된 본문을 변환할 때 키를 래핑할 수 없습니다.
3605 | ErrorWrapKeyBase64EncodeKey | 키를 Base64 인코딩하지 못해 키를 래핑할 수 없습니다.
3606 | ErrorWrapKeyBase64DecodeValue | 응답 값을 Base64로 디코딩하지 못해 키를 래핑할 수 없습니다.
3607 | ErrorWrapKeyJsonParser | JSON 응답을 구문 분석하지 못해 키를 래핑할 수 없습니다.
3608 | ErrorWrapKeyExtractValue | 응답에서 값을 추출하지 못해 키를 래핑할 수 없습니다.
3609 | ErrorWrapKeyNoResponse | 서버로부터 응답이 없기 때문에 키를 래핑할 수 없습니다.
3700 | ErrorUnwrapKeyOutOfMemoryConvertResponseString | 메모리 부족으로 인해 응답 문자열을 변환할 때 키를 래핑 해제할 수 없습니다.
3701 | ErrorUnwrapKeyOutOfMemoryConcatPath | 메모리 부족으로 인해 경로를 연결할 때 키를 래핑 해제할 수 없습니다.
3702 | ErrorUnwrapKeyOutOfMemoryConcatHeader | 메모리 부족으로 인해 헤더를 연결할 때 키를 래핑 해제할 수 없습니다.
3703 | ErrorUnwrapKeyOutOfMemoryConcatBody | 메모리 부족으로 인해 본문을 연결할 때 키를 래핑 해제할 수 없습니다.
3704 | ErrorUnwrapKeyOutOfMemoryConvertEncodedBody | 메모리 부족으로 인해 인코딩된 본문을 변환할 때 키를 래핑 해제할 수 없습니다.
3705 | ErrorUnwrapKeyBase64EncodeKey | 키를 Base64 인코딩하지 못해 키를 래핑 해제할 수 없습니다.
3706 | ErrorUnwrapKeyBase64DecodeValue | 응답 값을 Base64로 디코딩하지 못해 키를 래핑 해제할 수 없습니다.
3707 | ErrorUnwrapKeyJsonParser | 응답에서 값을 추출하지 못해 키를 래핑 해제할 수 없습니다.
3708 | ErrorUnwrapKeyExtractValue | 응답에서 값을 추출하지 못해 키를 래핑 해제할 수 없습니다.
3709 | ErrorUnwrapKeyNoResponse | 서버로부터 응답이 없기 때문에 키를 래핑 해제할 수 없습니다.
3800 | ErrorSecretAuthParamsGetRequestBody | AAD 클라이언트 ID 및 비밀을 사용하여 요청 본문을 만드는 동안 오류가 발생했습니다.
3801 | ErrorJWTTokenCreateHeader | AAD를 사용한 인증을 위해 JWT 토큰 헤더를 만드는 동안 오류가 발생했습니다.
3802 | ErrorJWTTokenCreatePayloadGUID | AAD를 사용한 인증을 위해 JWT 토큰 페이로드의 GUID를 만드는 동안 오류가 발생했습니다.
3803 | ErrorJWTTokenCreatePayload | AAD를 사용한 인증을 위해 JWT 토큰 페이로드를 만드는 동안 오류가 발생했습니다.
3804 | ErrorJWTTokenCreateSignature | AAD를 사용한 인증을 위해 JWT 토큰 서명을 만드는 동안 오류가 발생했습니다.
3805 | ErrorJWTTokenSignatureHashAlg | AAD를 사용한 인증을 위해 SHA256 해시 알고리즘을 가져오는 동안 오류가 발생했습니다.
3806 | ErrorJWTTokenSignatureHash | AAD를 사용한 JWT 토큰 인증을 위해 SHA256 해시를 만드는 동안 오류가 발생했습니다.
3807 | ErrorJWTTokenSignatureSignHash | AAD를 사용한 인증을 위해 JWT 토큰 해시에 서명하는 동안 오류가 발생했습니다.
3808 | ErrorJWTTokenCreateToken | AAD를 사용한 인증을 위해 JWT 토큰을 만드는 동안 오류가 발생했습니다.
3809 | ErrorPfxCertAuthParamsImportPfx | AAD를 사용한 인증을 위해 Pfx 인증서를 가져오는 동안 오류가 발생했습니다.
3810 | ErrorPfxCertAuthParamsGetThumbprint | AAD를 사용한 인증을 위해 Pfx 인증서에서 지문을 가져오는 동안 오류가 발생했습니다.
3811 | ErrorPfxCertAuthParamsGetPrivateKey | AAD를 사용한 인증을 위해 Pfx 인증서에서 프라이빗 키를 가져오는 동안 오류가 발생했습니다.
3812 | ErrorPfxCertAuthParamsSignAlg | AAD를 사용한 Pfx 인증서 인증을 위해 RSA 서명 알고리즘을 가져오는 동안 오류가 발생했습니다.
3813 | ErrorPfxCertAuthParamsImportForSign | AAD를 사용한 인증을 위해 RSA 서명용 Pfx 프라이빗 키를 가져오는 동안 오류가 발생했습니다.
3814 | ErrorPfxCertAuthParamsCreateRequestBody | AAD를 사용한 인증을 위해 Pfx 인증서에서 요청 본문을 만드는 동안 오류가 발생했습니다.
3815 | ErrorPEMCertAuthParamsGetThumbprint | AAD를 사용한 인증을 위해 지문을 Base64 디코딩하는 동안 오류가 발생했습니다.
3816 | ErrorPEMCertAuthParamsGetPrivateKey | AAD를 사용한 인증을 위해 PEM에서 RSA 프라이빗 키를 가져오는 동안 오류가 발생했습니다.
3817 | ErrorPEMCertAuthParamsSignAlg | AAD를 사용한 PEM 프라이빗 키 인증을 위해 RSA 서명 알고리즘을 가져오는 동안 오류가 발생했습니다.
3818 | ErrorPEMCertAuthParamsImportForSign | AAD를 사용한 인증을 위해 RSA 서명용 PEM 프라이빗 키를 가져오는 동안 오류가 발생했습니다.
3819 | ErrorPEMCertAuthParamsCreateRequestBody | AAD를 사용한 인증을 위해 PEM 프라이빗 키에서 요청 본문을 만드는 동안 오류가 발생했습니다.
3820 | ErrorLegacyPrivateKeyAuthParamsSignAlg | AAD를 사용한 레거시 프라이빗 키 인증을 위해 RSA 서명 알고리즘을 가져오는 동안 오류가 발생했습니다.
3821 | ErrorLegacyPrivateKeyAuthParamsImportForSign | AAD를 사용한 인증을 위해 RSA 서명용 레거시 프라이빗 키를 가져오는 동안 오류가 발생했습니다.
3822 | ErrorLegacyPrivateKeyAuthParamsCreateRequestBody        | AAD를 사용한 인증을 위해 레거시 프라이빗 키에서 요청 본문을 만드는 동안 오류가 발생했습니다.
3900 | ErrorAKVDoesNotExist | 오류 인터넷 이름이 확인되지 않았습니다. 이는 일반적으로 Azure Key Vault가 삭제되었음을 나타냅니다.
4000 | ErrorCreateKeyVaultRetryManagerOutOfMemory | 메모리 부족으로 인해 AKV 작업에 대한 RetryManager를 만들 수 없습니다.

이 테이블에 오류 코드가 표시되지 않는 경우 오류가 발생할 수 있는 일부 다른 이유는 다음과 같습니다.
  
- 인터넷 액세스 권한이 없으며 Azure Key Vault에 액세스할 수 없습니다. 인터넷 연결을 확인하세요.  
  
- Azure 주요 자격 증명 모음 서비스가 종료될 수 있습니다. 나중에 다시 시도하세요.  
  
- Azure 주요 자격 증명 모음 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 비대칭 키를 삭제했을 수 있습니다. 키를 복원하세요.  
  
- "라이브러리를 로드할 수 없습니다"라는 오류가 표시되는 경우 실행 중인 SQL Server 버전에 따라 재배포 가능한 Visual Studio C++의 적절한 버전이 설치되어 있는지 확인합니다. 다음 표에서는 Microsoft 다운로드 센터에서 설치할 버전을 지정합니다.

Windows 이벤트 로그는 SQL Server 커넥터와 관련된 오류도 기록하므로 오류가 실제로 발생하는 이유에 대한 추가 컨텍스트를 제공할 수 있습니다. Windows 애플리케이션 이벤트 로그의 원본은 “Microsoft Azure Key Vault용 SQL Server 커넥터”가 됩니다.
  
SQL Server 버전  |재배포 가능 설치 링크
---------|---------
2008, 2008 R2, 2012, 2014 | [Visual Studio 2013용 Visual C++ 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=40784)
2016 | [Visual Studio 2015용 Visual C++ 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=48145)
  
## <a name="additional-references"></a>추가 참조

 확장 가능 키 관리 추가 정보:  
  
- [확장 가능 키 관리 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 EKM을 지원하는 SQL 암호화:  
  
- [EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
- [백업 암호화](../../../relational-databases/backup-restore/backup-encryption.md)  
  
- [암호화된 백업 만들기](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 관련 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령:  
  
- [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
- [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
- [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
- [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
- [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
- [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
- [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Azure 주요 자격 증명 모음 설명서:  
  
- [Azure Key Vault란?](/azure/key-vault/general/basic-concepts)  
  
- [Azure 키 자격 증명 모음 시작](/azure/key-vault/general/overview)  
  
- PowerShell [Azure 주요 자격 증명 모음 Cmdlet](/powershell/module/azurerm.keyvault/) 참조  
  
## <a name="see-also"></a>참고 항목

 [Azure Key Vault를 사용한 확장 가능 키 관리](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)  
 [EKM provider enabled 서버 구성 옵션](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)

추가 샘플 스크립트는 [SQL Server 투명한 데이터 암호화 및 Azure Key Vault를 사용한 확장 가능 키 관리](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549) 블로그를 참조하세요.