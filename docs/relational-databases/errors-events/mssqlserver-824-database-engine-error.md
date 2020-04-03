---
title: MSSQLSERVER_824 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c3fa77a50b32541a4ed9b8742bebe04e4e735b45
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80342935"
---
# <a name="mssqlserver_824"></a>MSSQLSERVER_824
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|824|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|B_HARDSSERR|  
|메시지 텍스트|SQL Server에서 일관성 기반의 논리적인 I/O 오류가 검색되었습니다. %ls. 파일 '%ls'의 오프셋 %#016I64x에서 데이터베이스 ID %d에 있는 페이지 %S_PGID의 %S_MSG 중 이 오류가 발생했습니다.  자세한 내용은 SQL Server 오류 로그 또는 시스템 이벤트 로그의 추가 메시지에서 확인할 수 있습니다.|  
  
## <a name="symptom"></a>증상  


데이터베이스 페이지를 읽거나 쓴 후에 논리 일관성 확인이 실패한 경우 SQL Server 오류 로그 또는 Windows 애플리케이션 이벤트 로그에서 다음과 같은 오류 메시지를 보게 될 수 있습니다.
 
``` 
2009-11-02 15:46:42.90 spid51      Error: 824, Severity: 24, State: 2.
2009-11-02 15:46:42.90 spid51      SQL Server detected a logical consistency-based I/O error: incorrect pageid (expected 1:43686; actual 0:0). It occurred during a read of page (1:43686) in database ID 23 at offset 0x0000001554c000 in file 'H:\MSSQL.SQL2008\MSSQL\DATA\my_db.mdf'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.
```
 
애플리케이션이 데이터를 쿼리 또는 수정하는 동안 이 메시지가 발생하면 오류 메시지는 해당 애플리케이션으로 반환되고 데이터베이스 연결이 종료됩니다. 
  
## <a name="cause"></a>원인
이 오류는 Windows가 디스크에서 페이지를 성공적으로 읽었음을 보고하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 해당 페이지에서 잘못된 내용을 발견했음을 나타냅니다. 이 오류는 Windows에서 오류를 감지하지 못했다는 점만 제외하면 오류 823과 비슷합니다. 일반적으로 이 오류는 디스크 드라이브 실패, 디스크 펌웨어 문제, 잘못된 디바이스 드라이버 등 I/O 하위 시스템의 문제를 나타냅니다. I/O 오류에 대한 자세한 내용은 [Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))(Microsoft SQL Server I/O 기본 사항, 2장)를 참조하세요.  

SQL Server는 Windows API(예: ReadFile, WriteFile, ReadFileScatter, WriteFileGather)를 사용하여 파일 I/O 작업을 수행합니다. 해당 I/O 작업을 수행한 후 SQL Server는 해당 API 호출과 관련된 오류 상태를 검사합니다. 운영 체제 오류로 인해 API 호출이 실패하면 SQL Server는 오류 823을 보고합니다. Windows API 호출 자체는 성공했으나 I/O 작업에 의해 전송된 데이터에서 논리 일관성 문제가 발생한 경우가 있을 수 있습니다. 이러한 논리 일관성 문제는 오류 824를 통해 보고됩니다.
 
824 오류는 다음과 같은 정보를 포함합니다.

- 이 I/O 작업이 수행된 데이터베이스 파일
- 이 I/O 작업이 시도된 파일의 오프셋
- 이 파일이 속한 데이터베이스
- 이 I/O 작업과 관련된 페이지 번호
- 작업이 읽기 작업인지 아니면 쓰기 작업인지
- 실패한 논리 일관성 확인의 세부 정보(확인의 종류, 이 확인에 사용된 실제 값과 예상 값)
 
이러한 논리 일관성 확인은 데이터 전송에 사용된 데이터의 특정 핵심 측면이 I/O 작업 전반에서 유지되었는지 확인하기 위해 SQL Server가 추가로 수행하는 무결성 검사입니다. 이러한 검사에는 체크섬, 조각난 페이지, 짧은 전송, 잘못된 페이지 ID, 부실 읽기, 페이지 감사 실패 등이 있습니다. 수행되는 검사의 성격은 데이터베이스 및 서버 수준의 여러 구성 옵션에 따라 달라집니다. 
 
824 오류 메시지는 일반적으로 기본 스토리지 시스템이나 I/O 요청의 경로에 있는 하드웨어 또는 드라이버에 문제가 있음을 나타냅니다. 파일 시스템에 불일치가 있거나 데이터베이스 파일이 손상된 경우이 오류가 발생할 수 있습니다.

## <a name="resolution"></a>해결 방법  

824 오류가 발생한 경우 다음과 같은 해결 방법을 시도해 볼 수 있습니다. 

- msdb에서 [suspect_pages](../backup-restore/manage-the-suspect-pages-table-sql-server.md) 테이블을 검토하여 동일한 데이터베이스 또는 다른 데이터베이스에 이 문제가 발생하는 다른 페이지가 있는지 확인합니다.
- DBCC CHECKDB 명령을 사용하여 824 메시지에 보고된 볼륨에 있는 여러 데이터베이스의 일관성을 검사합니다. DBCC CHECKDB 명령에서 불일치를 발견한 경우에는 기술 자료 문서 [DBCC CHECKDB에서 보고된 데이터베이스 일관성 오류 문제를 해결하는 방법](https://support.microsoft.com/help/2015748/how-to-troubleshoot-database-consistency-errors-reported-by-dbcc-check)의 지침을 따르세요.
- 824 오류가 발생한 데이터베이스에서 PAGE_VERIFY CHECKSUM 데이터베이스 옵션이 설정되어 있지 않다면 즉시 이 옵션을 설정합니다. 824 오류는 체크섬 실패 외의 다른 이유로도 발생할 수 있지만, CHECKSUM은 페이지가 디스크에 쓰여진 후에 페이지의 일관성을 확인할 가장 좋은 옵션을 제공합니다.
- Windows 이벤트 로그에서 운영 체제나 스토리지 디바이스 또는 디바이스 드라이버에서 보고한 오류 또는 메시지를 검토합니다. 어떤 방식으로든 이 오류와 관련이 있을 경우 해당 오류를 먼저 해결하세요. 예를 들어 824 메시지와는 별도로, 디스크 원본에서 보고된 “\Device\Harddisk4\DR4에 컨트롤러 오류가 있습니다”와 같은 이벤트가 이벤트 로그에 표시될 수도 있습니다. 이 경우, 이 디바이스에 파일이 있는지 평가하고 해당 디스크 오류를 먼저 수정해야 합니다.
- [SQLIOSim](https://support.microsoft.com/help/231619/how-to-use-the-sqliosim-utility-to-simulate-sql-server-activity-on-a-d) 유틸리티를 사용하여 일반적인 SQL Server I/O 요청 외부에서 824 오류를 재현할 수 있는지 확인합니다. SQLIOSim은 SQL Server 2008과 함께 제공되므로 이 버전 이상에서는 별도로 다운로드할 필요가 없습니다.
- 하드웨어 공급업체 또는 디바이스 제조업체와 협력하여 다음을 확인합니다.
   - 하드웨어 디바이스와 구성이 [SQL Server의 I/O 요구 사항](https://support.microsoft.com/help/967576/microsoft-sql-server-database-engine-input-output-requirements)을 준수합니다.
   - I/O 경로에 있는 모든 디바이스의 디바이스 드라이버 및 기타 지원 소프트웨어 구성 요소가 최신 상태입니다.
- 하드웨어 공급업체 또는 디바이스 제조업체에서 진단 유틸리티를 제공한 경우 해당 유틸리티를 사용하여 I/O 시스템의 상태를 평가합니다.
- I/O 요청의 경로에 문제가 발생하는 필터 드라이버가 있는지 평가합니다.
   - 해당 필터 드라이버의 업데이트가 있는지 확인
   - 해당 필터 드라이버를 제거하거나 사용하지 않도록 설정하여 824 오류의 원인이 되는 문제가 사라지는지 확인
- 하드웨어 관련 문제가 아니면 정상적인 백업(있는 경우)을 사용하여 데이터베이스를 복원하십시오.  

## <a name="see-also"></a>참고 항목  
[suspect_pages 테이블 관리&#40;SQL Server&#41;](~/relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
