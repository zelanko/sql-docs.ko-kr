---
title: MSSQLSERVER_17204 | Microsoft 문서
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: 362f907187d7fe738216ea2000f2a5c48eca7b5f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780785"
---
# <a name="mssqlserver_17207"></a>MSSQLSERVER_17207
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |
| :-------- | :---- |
|제품 이름|SQL Server|  
|이벤트 ID|17207|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBLKIO_OS2DISKERROR|  
|메시지 텍스트|%ls: 파일 '%ls'을(를) 만들거나 여는 동안 운영 체제 오류 %ls이(가) 발생했습니다. 운영 체제 오류를 진단하고 수정한 후 작업을 다시 시도하십시오.|  


## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 지정된 OS 오류로 인해 지정된 파일을 열지 못했습니다.  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 데이터베이스 및/또는 트랜잭션 로그 파일을 열 수 없는 경우 Windows 애플리케이션 이벤트 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 오류 17207이 표시될 수 있습니다. 다음은 이 오류의 예입니다.

``` 
Error: 17207, Severity: 16, State: 1.
FileMgr::StartSecondaryDataFiles: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'F:\MSSQL\DATA\MyDB_FG1_1.ndf'. Diagnose and correct the operating system error, and retry the operation.
```

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 시작 프로세스 중 또는 데이터베이스를 시작하려는 모든 데이터베이스 작업(예: ALTER DATABASE) 중에 이러한 오류가 표시될 수 있습니다. 경우에 따라 17207 및 17204 오류가 모두 표시될 수도 있고 둘 중 하나만 표시될 수도 있습니다.

사용자 데이터베이스에 이러한 오류가 발생하면 해당 데이터베이스는 RECOVERY_PENDING 상태로 유지되고 애플리케이션은 데이터베이스에 액세스할 수 없습니다. 시스템 데이터베이스에 이러한 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작되지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 없습니다. 이로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 리소스가 오프라인 상태가 될 수도 있습니다.

문제가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FileStream 파일 그룹에 관련된 경우 파일 이름 대신 전체 디렉터리 경로만 나열됩니다. 다음 예를 참조하세요. 
```
Error: 17207, Severity: 16, State: 1.
STREAMFCB::Startup: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\bpa_files_test_fs_1\bpa_files_test_fs_1'. Diagnose and correct the operating system error, and retry the operation.
```

## <a name="cause"></a>원인
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 사용하려면 먼저 데이터베이스를 시작해야 합니다. 데이터베이스 시작 프로세스에는 데이터베이스 및 데이터베이스 파일을 나타내는 다양한 데이터 구조를 초기화하고, 데이터베이스에 속하는 모든 파일을 열고, 마지막으로 데이터베이스에서 복구를 실행하는 작업이 포함됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [CreateFile](https://docs.microsoft.com/windows/win32/api/fileapi/nf-fileapi-createfilea) Windows API 함수를 사용하여 데이터베이스에 속하는 파일을 엽니다.
 
메시지 17207(및 17204)은 시작 프로세스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 데이터베이스 파일을 열려고 할 때 오류가 발생했음을 표시합니다.
 
이러한 오류 메시지에는 다음 정보가 포함됩니다.
1. 파일을 열려고 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 함수의 이름. 일반적으로 이러한 오류 메시지에서 관찰되는 함수 이름은 다음 중 하나입니다.
   - FCB::Open                              - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 파일을 열려고 할 때 오류가 발생함
   - FileMgr::StartPrimaryDataFiles         - 주 파일 그룹에 속하는 주 데이터 파일 또는 파일
   - FileMgr::StartSecondaryDataFiles       - 보조 파일 그룹에 속하는 파일
   - FileMgr::StartLogFiles                 - 트랜잭션 로그 파일
   - STREAMFCB::Startup                     - SQL FileStream 컨테이너
   - FCB::RemoveAlternateStreams
  
      
1. 상태 정보는 이 오류 메시지를 생성할 수 있는 함수 내 여러 위치를 구분합니다.
1. 파일의 전체 실제 경로입니다.
1. 파일에 해당하는 파일 ID입니다.
1. 운영 체제 오류 코드 및 오류 설명입니다. 일부 경우에는 오류 코드만 표시됩니다.
 
이러한 오류 메시지에 출력되는 운영 체제 오류 정보는 17204 오류가 발생하는 근본 원인입니다. 이러한 오류 메시지의 일반적인 원인은 권한 문제 또는 잘못된 파일 경로입니다.


## <a name="user-action"></a>사용자 조치  
1. 17207 오류를 해결하려면 연결된 운영 체제 오류 코드를 이해하고 해당 오류를 진단해야 합니다. 운영 체제 오류 상태가 해결되면 데이터베이스(예를 들어 ALTER DATABASE SET ONLINE을 사용) 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작하여 영향을 받은 데이터베이스를 온라인 상태로 만들 수 있습니다. 일부 경우에는 운영 체제 오류를 해결할 수 없으므로 특정한 정정 작업을 수행해야 합니다. 이 섹션에서는 이러한 작업에 대해 설명합니다.
1. 17207 오류 메시지에 오류 코드만 포함되고 오류 설명이 없는 경우에는 운영 체제 셸에서 net helpmsg <error code> 명령을 사용하여 오류 코드를 해결할 수 있습니다. 오류 코드로 8자리 상태 코드가 반환되는 경우 [HRESULT를 Win32 오류 코드로 변환하는 방법은 무엇인가요?](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133)와 같은 정보 소스를 참조하여 이러한 상태 코드가 어떤 OS 오류인지 확인합니다.
1. ```Access is Denied``` 운영 체제 오류 = 5가 반환되는 경우 다음 방법을 고려하세요.
   -  Windows 탐색기에서 파일의 속성을 확인하여 파일에 설정된 권한을 확인합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Windows 그룹을 사용하여 다양한 파일 리소스에 액세스 제어를 프로비전합니다. (SQLServerMSSQLUser$ComputerName$MSSQLSERVER 또는 SQLServerMSSQLUser$ComputerName$InstanceName 같은 이름을 가진) 적절한 그룹에 오류 메시지에서 언급된 데이터베이스 파일에 필요한 권한이 있는지 확인합니다. 자세한 내용은 [데이터베이스 엔진 액세스에 대한 파일 시스템 권한 구성](../../2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md)을 검토하세요. Windows 그룹에 실제로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정 또는 서비스 SID가 포함되어 있는지 확인합니다.
   -  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 현재 실행되고 있는 사용자 계정을 검토합니다. Windows 작업 관리자를 사용하여 이 정보를 가져올 수 있습니다. 실행 파일 "sqlservr.exe"의 "사용자 이름" 값을 찾습니다. 또한 최근에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 변경한 경우 이 작업을 수행하는 데 지원되는 방법은 SQL Server 구성 관리자 유틸리티를 사용하는 것임을 알아야 합니다. 이에 대한 자세한 내용은 [SQL Server 구성 관리자](../sql-server-configuration-manager.md)에서 확인할 수 있습니다. 
   -  작업 유형(서버 시작 시 데이터베이스 열기, 데이터베이스 연결, 데이터베이스 복원 등)에 따라 가장과 데이터베이스 파일 액세스에 사용되는 계정이 다를 수 있습니다. [데이터 및 로그 파일 보안](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN) 항목을 검토하여 어떤 작업이 어떤 권한을 어떤 계정에 설정하는지 파악합니다. Windows SysInternals [프로세스 모니터](https://docs.microsoft.com/sysinternals/downloads/procmon)와 같은 도구를 사용하여 파일 액세스가 SQL Server 인스턴스 서비스 시작 계정(또는 서비스 SID) 또는 가장된 계정의 보안 컨텍스트에서 일어나는지 확인합니다.

      SQL Server가 ALTER DATABASE 또는 CREATE DATABASE 작업을 실행하는 로그인의 사용자 자격 증명을 가장하는 경우 프로세스 모니터 도구(예)에서 다음과 같은 정보를 확인할 수 있습니다.

        ```
        Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName
        ```
  
1. ```The system cannot find the file specified``` OS 오류 = 3이 표시되는 경우:
   - 오류 메시지에서 전체 경로를 검토합니다.
   - Windows 탐색기에서 디스크 드라이브 및 폴더 경로가 표시되고 액세스할 수 있는지 확인합니다.
   - Windows 이벤트 로그를 검토하여 이 디스크 드라이브에 문제가 있는지 확인합니다.
   - 경로가 올바르지 않고 이 데이터베이스가 시스템에 이미 존재한다면 [데이터베이스 파일 이동](../databases/move-database-files.md) 문서에서 설명하는 방법을 사용하여 데이터베이스 파일 경로를 변경할 수 있습니다. 이 프로시저를 반드시 사용해야 하는 경우가 있으며, 대표적인 경우는 시스템 데이터베이스 파일에서 17204 또는 17207이 발생하며 지정된 디스크 드라이브를 사용할 수 없는 재해 복구 시나리오를 작업하는 경우입니다. 이 항목에서는 다양한 시스템 데이터베이스[master, model, tempdb, msdb 및 mssqlsystemresource.mdf]의 현재 위치를 식별하는 방법도 설명합니다.
   - 데이터베이스 파일이 없기 때문에 이 오류가 표시된다면 유효한 백업에서 데이터베이스를 복원해야 합니다.
     - 오류와 연결된 데이터베이스 파일이 보조 파일 그룹에 속한다면 파일 그룹을 오프라인으로 표시하고 데이터베이스를 온라인으로 전환한 다음 해당 파일 그룹만 복원할 수도 있습니다. 자세한 내용은 [ALTER DATABASE 파일 및 파일 그룹 옵션(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 항목의 OFFLINE 섹션을 참조하세요.
     - 오류를 생성한 파일이 트랜잭션 로그 파일이라면 [CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) 항목의 "FOR ATTACH" 및 "FOR ATTACH_REBUILD_LOG" 섹션에서 정보를 검토하여 누락된 트랜잭션 로그 파일을 만드는 방법을 확인합니다.
   - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이러한 위치에 있는 데이터베이스 파일에 액세스하기 전에 [iSCSI 드라이브 같은] 디스크나 네트워크 위치를 사용할 수 있는지 확인합니다. 필요하다면 클러스터 관리자나 서비스 제어 관리자에서 필요한 종속성을 만듭니다.

1. ```The process cannot access the file because it is being used by another process``` 운영 체제 오류 = 32가 표시되는 경우:
   - Windows Sysinternals에서 [프로세스 탐색기](https://docs.microsoft.com/sysinternals/downloads/process-explorer)나 [핸들](https://docs.microsoft.com/sysinternals/downloads/handle) 같은 도구를 사용하여 다른 프로세스 또는 서비스가 이 데이터베이스 파일에 대한 배타적 잠금을 획득했는지 확인합니다.
   - 프로세스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일에 액세스하지 못하게 합니다. 일반적인 예제에는 바이러스 백신 프로그램이 동원됩니다(다음 [기술 자료 문서](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server)에서 파일 제외 지침을 참조하세요).
   - 클러스터 환경에서 이전 소유 노드의 sqlservr.exe 프로세스가 데이터베이스 핸들을 실제로 릴리스했는지 확인합니다. 일반적으로는 발생하지 않지만 클러스터 또는 I/O 경로를 잘못 구성하면 이러한 문제가 발생할 수 있습니다.
  
