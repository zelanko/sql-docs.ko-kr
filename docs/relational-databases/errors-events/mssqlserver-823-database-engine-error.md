---
title: MSSQLSERVER 오류 823  | mssqlserver_823
description: 데이터베이스 무결성을 위협하며 즉시 해결해야 하는 심각한 시스템 수준 오류 상태인 Microsoft SQL Server 오류 823(mssqlserver_823)에 대한 설명과 몇 가지 일반적인 해결 방법입니다.
ms.custom: ''
ms.date: 01/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f79710c168f87f1156f6bbce780f8fd154ea1dd0
ms.sourcegitcommit: 4b2c9d648b7a7bdf9c3052ebfeef182e2f9d66af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/04/2020
ms.locfileid: "77013108"
---
# <a name="mssqlserver-error-823"></a>MSSQLSERVER 오류 823
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|823|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|B_HARDERR|  
|메시지 텍스트|파일 '%ls'의 오프셋 %#016I64x에서 %S_MSG 중 운영 체제에서 SQL Server에 대한 오류 %ls을(를) 반환했습니다. SQL Server 오류 로그 및 시스템 이벤트 로그의 추가 메시지에서 더 자세한 정보를 얻을 수 있습니다. 이는 데이터베이스 무결성을 위협하는 심각한 시스템 수준의 오류 상태이며 즉시 수정해야 합니다. 전체 데이터베이스 일관성 확인(DBCC CHECKDB)을 완료하십시오. 이 오류는 여러 요인으로 인해 발생할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.|  
  
## <a name="explanation"></a>설명  
SQL Server는 Windows API(예: [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile), [WriteFile](/windows/win32/api/fileapi/nf-fileapi-writefile), [ReadFileScatter](/windows/win32/api/fileapi/nf-fileapi-readfilescatter), [WriteFileGather](/windows/win32/api/fileapi/nf-fileapi-writefilegather))를 사용하여 파일 I/O 작업을 수행합니다. 해당 I/O 작업을 수행한 후 SQL Server는 해당 API 호출과 관련된 오류 상태를 검사합니다. 운영 체제 오류로 인해 API 호출이 실패하면 SQL Server는 오류 823을 보고합니다.

 823 오류 메시지에는 다음 정보가 포함되어 있습니다.
 - I/O 작업이 수행된 데이터베이스 파일
 - I/O 작업이 시도된 파일 내의 오프셋. 파일 시작 부분에서의 실제 바이트 오프셋입니다. 이 숫자를 8192로 나누면 오류의 영향을 받는 논리 페이지 번호를 구할 수 있습니다.
 - I/O 작업이 읽기 또는 쓰기 요청인지 여부
 - 괄호 안에 표시되는 운영 체제 오류 코드 및 오류 설명
 

**운영 체제 오류:** 읽기 또는 쓰기 Windows API 호출이 실패하고, SQL Server에서 Windows API 호출과 관련된 운영 체제 오류가 발생합니다. 다음 메시지는 823 오류의 예입니다.

```
Error: 823, Severity: 24, State: 2.
2010-03-06 22:41:19.55 spid58 The operating system returned error 1117 (The request could not be performed because of an I/O device error.) to SQL Server during a read at offset 0x0000002d460000 in file 'e:\program files\Microsoft SQL Server\mssql\data\mydb.MDF'. Additional messages in the SQL Server error log and system event log may provide more detail. This is a severe, system-level error condition that threatens database integrity and must be corrected immediately. It is recommended to complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.
```

오류 메시지의 파일과 연결된 데이터베이스에 대한 DBCC CHECKDB 문에서 오류가 표시될 수도 있고, 표시되지 않을 수도 있습니다. 823 오류가 표시되면 DBCC CHECKDB 문을 실행할 수 있습니다. DBCC CHECKDB 문이 오류를 보고하지 않는 경우 일시적인 시스템 문제이거나 디스크 문제일 가능성이 큽니다.

추적 플래그 818을 사용하면 823 오류에 대한 추가 진단 정보가 SQL Server 오류 로그 파일에 기록될 수 있습니다.
자세한 내용은 [KB 826433: 보고되지 않은 I/O 문제를 검색하기 위해 SQL Server 진단 추가됨](https://support.microsoft.com/help/826433/sql-server-diagnostics-added-to-detect-unreported-i-o-problems-due-to)을 참조하세요.


## <a name="cause"></a>원인
823 오류 메시지는 일반적으로 기본 스토리지 시스템이나 I/O 요청의 경로에 있는 하드웨어 또는 드라이버에 문제가 있음을 나타냅니다. 파일 시스템에 불일치가 있거나 데이터베이스 파일이 손상된 경우이 오류가 발생할 수 있습니다. 파일 읽기의 경우, SQL Server에서 읽기 요청을 4회 다시 시도한 후에 823을 반환합니다. 다시 시도 작업이 성공하면 쿼리가 실패하지 않지만 메시지 [825](mssqlserver-825-database-engine-error.md)가 ERRORLOG 및 이벤트 로그에 기록됩니다.

## <a name="user-action"></a>사용자 동작  
 - MSDB의 [suspect_pages](../system-tables/suspect-pages-transact-sql.md) 테이블을 검토하여 동일한 데이터베이스 또는 다른 데이터베이스에서 이 문제가 발생하는 다른 페이지가 있는지 확인합니다.
 - DBCC CHECKDB 명령을 사용하여 823 메시지에 보고된 볼륨과 동일한 볼륨에 있는 데이터베이스의 일관성을 검사합니다. DBCC CHECKDB 명령에서 불일치를 발견한 경우에는 [DBCC CHECKB에서 보고된 데이터베이스 일관성 오류 문제를 해결하는 방법](https://support.microsoft.com/help/2015748/how-to-troubleshoot-database-consistency-errors-reported-by-dbcc-check)의 지침을 따르세요. 
 - Windows 이벤트 로그에서 운영 체제나 스토리지 디바이스 또는 디바이스 드라이버에서 보고한 오류 또는 메시지를 검토합니다. 어떤 방식으로든 이 오류와 관련이 있을 경우 해당 오류를 먼저 해결합니다. 예를 들어 823 메시지와는 별도로, 디스크 원본에서 보고된 “드라이버가 \Device\Harddisk4\DR4에서 컨트롤러 오류를 검색했습니다.”와 같은 이벤트가 이벤트 로그에 표시될 수도 있습니다. 이 경우, 이 디바이스에 파일이 있는지 평가하고 해당 디스크 오류를 먼저 수정해야 합니다.
 - [SQLIOSim](https://support.microsoft.com/help/231619/how-to-use-the-sqliosim-utility-to-simulate-sql-server-activity-on-a-d) 유틸리티를 사용하여 일반적인 SQL Server I/O 요청 외부에서 해당 823 오류를 재현할 수 있는지 확인합니다. SQLIOSim 유틸리티는 SQL Server 2008 이상 버전과 함께 제공되므로 별도로 다운로드할 필요가 없습니다. 일반적으로 `C:\Program Files\Microsoft SQL Server\MSSQLxx.MSSQLSERVER\MSSQL\Binn` 폴더에서 찾을 수 있습니다.
 - 하드웨어 공급업체 또는 디바이스 제조업체와 협력하여 다음을 확인합니다.
   - 하드웨어 디바이스와 구성이 SQL Server의 I/O 요구 사항을 준수함
   - I/O 경로에 있는 모든 디바이스의 디바이스 드라이버 및 기타 지원 소프트웨어 구성 요소가 최신 상태임
 - 하드웨어 공급업체 또는 디바이스 제조업체에서 진단 유틸리티를 제공한 경우 해당 유틸리티를 사용하여 I/O 시스템의 상태를 평가합니다.
 - 문제가 발생하는 I/O 요청의 경로에 존재하는 [필터 드라이버](https://support.microsoft.com/help/2454053/use-of-system-filter-drivers-can-lead-to-sql-server-database-engine-pe)가 있는지 평가합니다.
   - 해당 필터 드라이버의 업데이트가 있는지 확인
   - 해당 필터 드라이버를 제거하거나 사용하지 않도록 설정하여 823 오류의 원인이 되는 문제가 사라지는지 확인할 수 있음  
