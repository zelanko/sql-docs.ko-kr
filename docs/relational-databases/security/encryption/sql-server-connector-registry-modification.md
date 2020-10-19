---
title: SQL Server 커넥터 오류 및 정보 로깅
description: 이 문서에서는 레지스트리 항목을 수정하여 SQL Server 커넥터 오류 및 로깅을 사용하도록 설정하는 방법을 설명합니다.
ms.date: 10/08/2020
ms.localizationpriority: medium
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: how-to
author: rupp29
ms.author: arupp
ms.openlocfilehash: 85be425e0e352961841f5317c7db219153a6c008
ms.sourcegitcommit: 9122251ab8bbd46ea3c699e741d6842c995195fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91847791"
---
# <a name="sql-server-connector-error-and-information-logging"></a>SQL Server 커넥터 오류 및 정보 로깅

이 문서에서는 레지스트리 항목을 수정하여 SQL Server 커넥터 오류 및 정보 로깅을 사용하도록 설정하는 방법을 설명합니다.

## <a name="sql-server-connector-for-microsoft-azure-key-vault"></a>Microsoft Azure Key Vault용 SQL Server 커넥터

[Microsoft Azure 주요 자격 증명 모음용 SQL Server 커넥터](https://www.microsoft.com/download/details.aspx?id=45344)를 사용하면 SQL Server 암호화에서 Microsoft Azure Key Vault를 EKM(확장 가능 키 관리) 공급자로 활용하여 암호화 키를 보호할 수 있습니다.

[다운로드](https://www.microsoft.com/download/details.aspx?id=45344)는 SQL Server 커넥터뿐 아니라 SQL Server 관리자가 SQL Server 커넥터를 구성하고 SQL Server 암호화 시나리오를 사용하도록 설정하는 방법을 배울 수 있는 샘플 스크립트로 구성되어 있습니다. 자세한 내용은 [Key Vault를 사용한 확장 가능 키 관리(SQL Server)](https://go.microsoft.com/fwlink/p/?LinkId=521690)를 참조하세요.

[Azure Key Vault 포럼](https://social.msdn.microsoft.com/Forums/AzureKeyVault)을 사용하여 질문하고, 인사이트를 공유하고, SQL Server 커넥터에 대해 논의합니다.

> [!NOTE]
> 정상적으로 실행되는 동안 SQL Server 커넥터 DLL은 Azure Key Vault에 연결하여 `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQL Server Cryptographic Provider]` 키를 만들기 위해 레지스트리 항목을 동적으로 만듭니다. SQL Server 시작 계정이 로컬 관리자여야 하거나, 해당 서비스 계정이 **NT SERVICE\MSSQLSERVER**여야 합니다.

## <a name="upgrade-sql-server-connector-to-the-latest-version"></a>최신 버전으로 SQL Server 커넥터 업그레이드

SQL Server 커넥터(버전: 1.0.5.0 - 날짜 2020년 9월)를 최신 버전의 DLL 암호화 공급자로 업그레이드하려면 다음 단계를 수행합니다.

### <a name="upgrade"></a>업그레이드

1. SQL Server 구성 관리자를 사용하여 SQL Server 서비스를 중지합니다.
1. **제어판\프로그램\프로그램 및 기능**을 사용하여 이전 버전을 제거합니다.
    1. 애플리케이션 이름: Microsoft Azure Key Vault용 SQL Server 커넥터
    1. 버전: 15.0.300.96
    1. DLL 파일 날짜: 2018-01-30 오후 3:00
1. 새로운 Microsoft Azure 주요 자격 증명 모음용 SQL Server 커넥터를 설치(업그레이드)합니다.
    1. 버전: 15.0.2000.367
    1. DLL 파일 날짜: 2020-09-11 ‏‎오전 5:17
1. SQL Server 서비스를 시작합니다.
1. 암호화된 DB에 액세스할 수 있는지 테스트합니다.

### <a name="rollback"></a>롤백

1. SQL Server 구성 관리자를 사용하여 SQL Server 서비스를 중지합니다.
1. **제어판\프로그램\프로그램 및 기능**을 사용하여 새 버전을 제거합니다.
    1. 애플리케이션 이름: Microsoft Azure Key Vault용 SQL Server 커넥터
    1. 버전: 15.0.2000.367
    1. DLL 파일 날짜: 2020-09-11 ‏‎오전 5:17
1. 이전 버전의 Microsoft Azure 주요 자격 증명 모음용 SQL Server 커넥터를 설치합니다.
    1. 버전: 15.0.300.96
    1. DLL 파일 날짜: 2018-01-30 오후 3:00
1. SQL Server 서비스를 시작합니다.
1. 암호화된 DB에 액세스할 수 있는지 테스트합니다.

> [!NOTE]
> - SQL Server 커넥터 버전 1.0.0.440 및 이전 버전은 대체되었으며 프로덕션 환경에서 더 이상 지원되지 않습니다. SQL Server 커넥터 문제를 해결하는 방법에 대한 자세한 내용은 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)을 참조하세요.
> - 1\.0.3.0 버전부터 SQL Server 커넥터는 문제를 해결하기 위해 Windows 이벤트 로그에 관련 오류 메시지를 보고합니다.
> - [1.0.4.0(버전 13.0.811.168)](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/SQLServerConnectorforMicrosoftAzureKeyVault.msi)부터 Azure 중국, Azure 독일, Azure Government 등의 프라이빗 Azure 클라우드가 지원됩니다.
> - 1\.0.5.0 버전의 경우 지문 알고리즘 측면에서 호환성이 손상되는 변경이 있습니다. 1\.0.5.0으로 업그레이드한 후 데이터베이스 복원 실패가 발생할 수 있습니다. 자세한 내용은 [기술 자료 문서 447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0)를 참조하세요.
> - **버전 1.0.5.0(파일 날짜 2020년 9월)부터 SQL Server 커넥터는 메시지 필터링 및 네트워크 요청 다시 시도 논리를 지원합니다.**
> - ‘이전 버전의 SQL Server 커넥터도 버전: [1.0.5.0(버전 15.0.300.96) – 파일 날짜 2018년 1월](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/ENU/SQLServerConnectorforMicrosoftAzureKeyVault.msi)’입니다. 이슈가 발생할 경우 최신 SQL Server 커넥터로 업그레이드합니다.

**시스템 요구 사항** - 지원되는 SQL Server 버전:

- SQL Server 2019 RTM Enterprise 64비트
- SQL Server 2017 RTM Enterprise 64비트
- SQL Server 2016 RTM Enterprise 64비트
- SQL Server 2014 RTM Enterprise 64비트
- SQL Server 2012 SP2 Enterprise 64비트
- SQL Server 2012 SP1 CU6 Enterprise 64비트
- SQL Server 2008 R2 SP2 CU8 Enterprise 64비트

위에 나열된 버전보다 낮은 SQL Server 2008 및 2012 버전에서는 다음 KB 문서에 지정된 패치를 설치해야 합니다. [https://support2.microsoft.com/kb/2859713](https://support2.microsoft.com/kb/2859713).

Microsoft Azure 주요 자격 증명 모음용 SQL Server 커넥터를 사용하려면 Azure의 Microsoft SQL Server Virtual Machine에 .NET 버전 4.5.1도 필요합니다. SQL Server 커넥터를 설치하기 전에 이 라이브러리를 설치해야 합니다.

실행하는 SQL Server 버전을 기준으로 적절한 버전의 Visual Studio C++ 재배포 가능 패키지를 설치합니다.

- SQL Server 버전 2008, 2008 R2, 2012, 2014의 경우 2013 Visual C++ 재배포 가능 패키지를 설치합니다.

- SQL Server 2016의 경우 2015 Visual C++ 재배포 가능 패키지를 설치합니다.

## <a name="modify-windows-registry-steps"></a>Windows 레지스트리 수정 단계

레지스트리 항목을 수정하여 Windows 애플리케이션 이벤트 로그에서 SQL Server 커넥터 로깅 오류 및 정보 이벤트를 사용하도록 설정합니다.

> [!CAUTION]
> 이 섹션의 단계를 신중하게 수행합니다. 위험에 대한 책임은 사용자에게 있습니다. 레지스트리를 잘못 수정하면 심각한 문제가 발생할 수 있습니다. 레지스트리를 수정하기 전에 문제가 발생할 경우 [복원하기 위해 레지스트리를 백업](https://support.microsoft.com/help/322756)합니다.

1. Windows 10에서 레지스트리 편집기를 여는 방법에는 다음 두 가지가 있습니다.
    - 작업 표시줄의 검색 상자에 **regedit**를 입력합니다. 레지스트리 편집기(데스크톱 앱)의 최상위 결과를 선택합니다.

    ![ekm regedit open](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-open.png "ekm regedit open")
    - 시작 단추를 길게 누르거나 마우스 오른쪽 단추로 클릭하고 실행을 선택합니다. 대화 상자에 **regedit**를 입력하고 **확인**을 선택합니다.

   ![ekm regedit start](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-start.png "ekm regedit start")

1. 다음 레지스트리 키로 이동합니다.

    **HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\\**

    ![ekm regedit akv](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv.png "ekm regedit akv")  

1. **Azure Key Vault** 아래에 `Log`라는 새 키를 추가합니다.

    **HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\\Log\\**

    ![ekm regedit akv log](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv-log.png "ekm regedit akv log.png")  

1. **Log** 키 아래에 `Level`이라는 DWORD(32비트) 값을 추가합니다.

    **HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\\Log\\**

    ![ekm regedit akv log dword](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv-log-dword.png "ekm regedit akv log dword")  

1. DWORD 값을 적절한 로그 수준(0, 1, 2)으로 설정합니다.
   1. 0(정보) - **기본값**
   1. 1(오류)
   1. 2(로그 없음)

   ![ekm regedit akv log level](../../../relational-databases/security/encryption/media/ekm-registry/ekm-regedit-akv-log-level.png "ekm regedit akv log level")  

이 문서에서 설명하는 레지스트리 항목은 다음 키 아래에 있습니다.

```console
\Computer
    \HKEY_LOCAL_MACHINE
       \SOFTWARE
          \Microsoft
             \SQL Server Cryptographic Provider
                \Azure Key Vault
                   \Log\
                      <Level>
```

필요에 따라 명령줄을 사용하여 키를 생성할 수 있습니다.

```cmd
--Create the logging parameter using (Administrator) Command Line:
REG ADD "HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\Log" /v Level /t REG_DWORD /d 1 

--Validate the new registry entry
REG QUERY "HKLM\SOFTWARE\Microsoft\SQL Server Cryptographic Provider\Azure Key Vault\Log" /v Level
```

메시지가 누락된 애플리케이션 이벤트 로그 항목도 레지스트리 항목을 사용하여 수정할 수 있습니다. 이벤트 로그에 `The description for Event ID 0 from source SQL Server Connector for Microsoft Azure Key Vault cannot be found...` 메시지가 포함될 수 있습니다.  

```cmd
--Create the registry entry to enable missing messages (this works with any version)
REG ADD "HKLM\SYSTEM\ControlSet001\Services\EventLog\Application\SQL Server Connector for Microsoft Azure Key Vault" /v EventMessageFile /t REG_EXPAND_SZ /d "C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll"

--Validate the new registry entry
REG QUERY "HKLM\SYSTEM\ControlSet001\Services\EventLog\Application\SQL Server Connector for Microsoft Azure Key Vault" /v EventMessageFile
```

## <a name="related-articles"></a>관련된 문서

- 추가 샘플 스크립트는 [SQL Server 투명한 데이터 암호화 및 Azure Key Vault를 사용한 확장 가능 키 관리](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549) 블로그를 참조하세요.
- [EKM(확장 가능 키 관리)](extensible-key-management-ekm.md)  
- [Azure Key Vault를 사용한 확장 가능 키 관리](extensible-key-management-using-azure-key-vault-sql-server.md)
- [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
