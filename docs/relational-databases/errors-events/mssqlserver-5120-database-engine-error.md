---
description: MSSQLSERVER_5120
title: MSSQLSERVER_5120
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5120 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: 368fba2b9f56af0b86741db0d15ceebcc238ab52
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869436"
---
# <a name="mssqlserver_5120"></a>MSSQLSERVER_5120
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|5120|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DSK_FCB_FAILURE|  
|메시지 텍스트|테이블 오류: 물리적 파일 "%.*ls"을(를) 열 수 없습니다. 운영 체제 오류 %d: "%ls".|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 데이터베이스 파일을 열지 못했습니다.  메시지에 제공된 운영 체제 오류는 보다 구체적인 실패 원인을 가리킵니다. 일반적으로 이 오류는 [17204](mssqlserver-17204-database-engine-error.md) 또는 [17207](mssqlserver-17207-database-engine-error.md)과 같은 다른 오류와 함께 표시될 수 있습니다.
  
## <a name="user-action"></a>사용자 조치  
  
  운영 체제 오류를 진단하고 수정한 후 작업을 다시 시도하세요. Microsoft가 제품에서 이 오류가 발생하는 영역 범위를 좁히는 데 도움이 되는 여러 가지 상태가 있습니다. 
  
### <a name="access-is-denied"></a>액세스 거부됨 
`Access is Denied` 운영 체제 오류 = 5가 반환되는 경우 다음 방법을 고려하세요.
   -  Windows 탐색기에서 파일의 속성을 보고 파일에 설정된 권한을 확인합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Windows 그룹을 사용하여 다양한 파일 리소스에 Access Control을 프로비전합니다. [SQLServerMSSQLUser$ComputerName$MSSQLSERVER 또는 SQLServerMSSQLUser$ComputerName$InstanceName 같은 이름을 가진] 적절한 그룹에 오류 메시지에서 언급된 데이터베이스 파일에 필요한 권한이 있는지 확인합니다. 자세한 내용은 [데이터베이스 엔진 액세스에 대한 파일 시스템 권한 구성](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access?view=sql-server-2014)을 검토하세요. Windows 그룹에 실제로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정 또는 서비스 SID가 포함되어 있는지 확인합니다.
   -  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 현재 실행되고 있는 사용자 계정을 검토합니다. Windows 작업 관리자를 사용하여 이 정보를 가져올 수 있습니다. 실행 파일 "sqlservr.exe"의 "사용자 이름" 값을 찾습니다. 또한 최근에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 변경한 경우 이 작업을 수행하는 데 지원되는 방법은 [SQL Server 구성 관리자](../sql-server-configuration-manager.md) 유틸리티를 사용하는 것임을 알아야 합니다. 
   -  작업 유형(서버 시작 시 데이터베이스 열기, 데이터베이스 연결, 데이터베이스 복원 등)에 따라 가장과 데이터베이스 파일 액세스에 사용되는 계정이 다를 수 있습니다. [데이터 및 로그 파일 보안](/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)) 항목을 검토하여 어떤 작업이 어떤 권한을 어떤 계정에 설정하는지 파악합니다. Windows SysInternals [프로세스 모니터](/sysinternals/downloads/procmon)와 같은 도구를 사용하여 파일 액세스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 서비스 시작 계정(또는 서비스 SID) 또는 가장된 계정의 보안 컨텍스트에서 일어나는지 확인합니다.

      [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 ALTER DATABASE 또는 CREATE DATABASE 작업을 실행하는 로그인의 사용자 자격 증명을 가장하는 경우 프로세스 모니터 도구(예)에서 다음과 같은 정보를 확인할 수 있습니다.
      
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
  
  
### <a name="attaching-files-that-reside-on-a-network-attached-storage"></a>네트워크 연결 스토리지에 있는 파일 연결  
네트워크 연결 스토리지에 있는 데이터베이스를 다시 연결할 수 없는 경우 애플리케이션 로그에 다음과 같은 메시지가 기록될 수 있습니다.

`Msg 5120, Level 16, State 101, Line 1 Unable to open the physical file "\\servername\sharename\filename.mdf". Operating system error 5: (Access is denied.).`

이 문제는 데이터베이스가 분리되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 파일 사용 권한을 다시 설정하기 때문에 발생합니다. 데이터베이스를 다시 연결하려고 하면 제한된 공유 권한으로 인해 오류가 발생합니다.

이 문제를 해결하려면 다음 단계를 수행합니다.
1. -T 시작 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작합니다. 이 시작 옵션을 사용하여 [SQL Server 구성 관리자](../sql-server-configuration-manager.md)에서 추적 플래그 1802를 설정합니다. 1802에 대한 자세한 내용은 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)를 참조하세요. 시작 매개 변수를 변경하는 방법에 대한 자세한 내용은 [데이터베이스 엔진 서비스 시작 옵션](../../database-engine/configure-windows/database-engine-service-startup-options.md)을 참조하세요.

2. 다음 명령을 사용하여 데이터베이스를 분리합니다.
   ```sql
    exec sp_detach_db DatabaseName
    go 
   ```

3. 다음 명령을 사용하여 데이터베이스를 다시 연결합니다.
   ```sql
   exec sp_attach_db DatabaseName, '\\Network-attached storage_Path\DatabaseMDFFile.mdf', '\\Network-attached storage_Path\DatabaseLDFFile.ldf'
   go
   ```
