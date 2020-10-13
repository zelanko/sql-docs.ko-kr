---
description: MSSQLSERVER_17204
title: MSSQLSERVER_17204 | Microsoft 문서
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d0dafe59102083ea1cd5c675819487eb88c9ecbc
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869485"
---
# <a name="mssqlserver_17204"></a>MSSQLSERVER_17204
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |
| :-------- | :---- |
|제품 이름|SQL Server|  
|이벤트 ID|17204|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBLKIO_DEVOPENFAILED|  
|메시지 텍스트|%ls: 파일 번호 %d에 대한 파일 %ls을(를) 열 수 없습니다.  OS 오류: '%ls'.|  
  
## <a name="explanation"></a>설명  
SQL Server가 지정된 OS 오류로 인해 지정된 파일을 열지 못했습니다.  

SQL Server가 데이터베이스 및/또는 트랜잭션 로그 파일을 열 수 없는 경우 Windows 애플리케이션 이벤트 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 오류 17204가 표시될 수 있습니다. 다음은 이 오류의 예입니다.

``` 
Error: 17204, Severity: 16, State: 1.
FCB::Open failed: Could not open file c:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\data\MyDB_Prm.mdf for file number 1.  OS error: 5(Access is denied.).
```

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 시작 프로세스 중 또는 데이터베이스를 시작하려는 모든 데이터베이스 작업(예: ALTER DATABASE) 중에 이러한 오류가 표시될 수 있습니다. 경우에 따라 17204 및 17207 오류가 모두 표시될 수도 있고 둘 중 하나만 표시될 수도 있습니다.

사용자 데이터베이스에 이러한 오류가 발생하면 해당 데이터베이스는 RECOVERY_PENDING 상태로 유지되고 애플리케이션은 데이터베이스에 액세스할 수 없습니다. 시스템 데이터베이스에 이러한 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작되지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 없습니다. 시스템 데이터베이스에 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 리소스가 오프라인 상태가 될 수도 있습니다.

## <a name="cause"></a>원인
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 사용하려면 먼저 데이터베이스를 시작해야 합니다. 데이터베이스 시작 프로세스에는 다음 작업이 포함됩니다. 
1. 데이터베이스 및 데이터베이스 파일을 나타내는 다양한 데이터 구조 초기화
1. 데이터베이스에 속한 모든 파일 열기
1. 데이터베이스에서 복구 실행 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [CreateFile](/windows/win32/api/fileapi/nf-fileapi-createfilea) Windows API 함수를 사용하여 데이터베이스에 속하는 파일을 엽니다.
 
메시지 17204(및 17207)는 시작 프로세스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 데이터베이스 파일을 열려고 할 때 오류가 발생했음을 표시합니다.
 
이러한 오류 메시지에는 다음 정보가 포함됩니다.
1. 파일을 열려고 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 함수의 이름. 일반적으로 이러한 오류 메시지에서 관찰되는 함수 이름은 다음 중 하나입니다.
   - FCB::Open - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 파일을 열려고 할 때 오류가 발생함
   - FileMgr::StartPrimaryDataFiles - 주 파일 그룹에 속하는 주 데이터 파일 또는 파일
   - FileMgr::StartSecondaryDataFiles - 보조 파일 그룹에 속하는 파일
   - FileMgr::StartLogFiles - 트랜잭션 로그 파일
   - STREAMFCB::Startup - SQL FileStream 컨테이너
   - FCB::RemoveAlternateStreams
  
      
1. 함수 내에서 이 오류 메시지를 생성할 수 있는 여러 위치를 구분하는 상태 정보
1. 파일의 전체 실제 경로
1. 파일에 해당하는 파일 ID
1. 운영 체제 오류 코드 및 오류 설명. 일부 경우에는 오류 코드만 표시됩니다.
 
이러한 오류 메시지에 출력되는 운영 체제 오류 정보는 17204 오류가 발생하는 근본 원인입니다. 이러한 오류 메시지의 일반적인 원인은 권한 문제 또는 잘못된 파일 경로입니다.


## <a name="user-action"></a>사용자 동작  
1. 17204 오류를 해결하려면 연결된 운영 체제 오류 코드를 이해하고 해당 오류를 진단해야 합니다. 운영 체제 오류 상태가 해결되면 데이터베이스(예를 들어 ALTER DATABASE SET ONLINE을 사용) 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작하여 영향을 받은 데이터베이스를 온라인 상태로 만들 수 있습니다. 운영 체제 오류를 해결할 수 없는 경우도 있습니다. 그러면 특정 정정 작업을 수행해야 합니다. 이 섹션에서는 이러한 작업에 대해 설명합니다.
1. 17204 오류 메시지에 오류 코드만 포함되고 오류 설명이 없는 경우에는 운영 체제 셸에서 net helpmsg <error code> 명령을 사용하여 오류 코드를 해결할 수 있습니다. 오류 코드로 8자리 상태 코드가 반환되는 경우 [HRESULT를 Win32 오류 코드로 변환하는 방법은 무엇인가요?](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133)와 같은 정보 소스를 참조하여 이러한 상태 코드가 어떤 OS 오류인지 확인합니다.
1. `Access is Denied` 운영 체제 오류 = 5가 반환되는 경우 다음 방법을 고려하세요.
   -  Windows 탐색기에서 파일의 속성을 보고 파일에 설정된 권한을 확인합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Windows 그룹을 사용하여 다양한 파일 리소스에 Access Control을 프로비전합니다. [SQLServerMSSQLUser$ComputerName$MSSQLSERVER 또는 SQLServerMSSQLUser$ComputerName$InstanceName 같은 이름을 가진] 적절한 그룹에 오류 메시지에서 언급된 데이터베이스 파일에 필요한 권한이 있는지 확인합니다. 자세한 내용은 [데이터베이스 엔진 액세스에 대한 파일 시스템 권한 구성](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access?view=sql-server-2014)을 검토하세요. Windows 그룹에 실제로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정 또는 서비스 SID가 포함되어 있는지 확인합니다.
   -  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 현재 실행되고 있는 사용자 계정을 검토합니다. Windows 작업 관리자를 사용하여 이 정보를 가져올 수 있습니다. 실행 파일 "sqlservr.exe"의 "사용자 이름" 값을 찾습니다. 또한 최근에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 변경한 경우 이 작업을 수행하는 데 지원되는 방법은 SQL Server 구성 관리자 유틸리티를 사용하는 것임을 알아야 합니다. 이에 대한 자세한 내용은 [SQL Server 구성 관리자](../sql-server-configuration-manager.md)에서 확인할 수 있습니다. 
   -  작업 유형(서버 시작 시 데이터베이스 열기, 데이터베이스 연결, 데이터베이스 복원 등)에 따라 가장과 데이터베이스 파일 액세스에 사용되는 계정이 다를 수 있습니다. [데이터 및 로그 파일 보안](/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)) 항목을 검토하여 어떤 작업이 어떤 권한을 어떤 계정에 설정하는지 파악합니다. Windows SysInternals [프로세스 모니터](/sysinternals/downloads/procmon)와 같은 도구를 사용하여 파일 액세스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 서비스 시작 계정(또는 서비스 SID) 또는 가장된 계정의 보안 컨텍스트에서 일어나는지 확인합니다.

      [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 ALTER DATABASE 또는 CREATE DATABASE 작업을 실행하는 사용자의 자격 증명을 가장하는 경우 프로세스 모니터 도구(예)에서 다음과 같은 정보를 확인할 수 있습니다.
        ```Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName```
  
1. If you are getting `The system cannot find the file specified` OS error = 3:
   - Review the complete path from the error message
   - Ensure the disk drive and the folder path is visible and accessible from Windows Explorer
   - Review the Windows Event log to find out if any problems exist with this disk drive
   - If the path is incorrect and if this database already exists in the system, you can change the database file paths using the methods explained in the topic [Move Database Files](../databases/move-database-files.md). You may have to use this procedure, especially for system database files that encounter 17204 or 17207 and you are working through a disaster recovery scenario where the specified disk drives are unavailable. This topic also explains how you can identify the current location of the various system databases [master, model, tempdb, msdb and mssqlsystemresource].
   - If you see this error because the database files are missing, you have to restore the database from a valid backup.
     - If the database file associated with the error belongs to a secondary filegroup, then you can optionally mark that filegroup offline, bring the database online and then perform a restore of that filegroup alone. For more information, refer to the OFFLINE section of the topic [ALTER DATABASE File and Filegroup Options (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).
     - If the file that produced the error is a transaction log file, review the information under the sections "FOR ATTACH" and "FOR ATTACH_REBUILD_LOG" of the topic [CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) to understand how you can recreate the missing transaction log files.
   - Ensure that any disk or network location [like iSCSI drive] is available before [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attempts to access the database files on these locations. If needed create the required dependencies in Cluster Administrator or Service Control Manager.
1. If you're getting the `The process cannot access the file because it is being used by another process` operating system error = 32:
   - Use a tool like [Process Explorer](/sysinternals/downloads/process-explorer) or [Handle](/sysinternals/downloads/handle) from Windows Sysinternals to find out if another process or service has acquired exclusive lock on this database file
   - Stop that process from accessing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database files. Common examples include anti-virus programs (see guidance for file exclusions in the following [KB article](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server) )
   - In a cluster environment, make sure that the sqlservr.exe process from the previous owning node has actually released the handles to the database files. Normally, this doesn't occur, but misconfigurations of the cluster or I/O paths can lead to such issues.
