---
title: MSSQLSERVER_605 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 605 (Database Engine error)
ms.assetid: d8d3a22e-1ff8-48a4-891f-4c8619437e24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 12e565fe5ad4c8e47187d50be50d9cd775b78ff3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751911"
---
# <a name="mssqlserver605"></a>MSSQLSERVER_605
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|605|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|WRONGPAGE|  
|메시지 텍스트|데이터베이스 %d에서 논리 페이지 %S_PGID을(를) 인출하지 못했습니다. 이 페이지는 할당 단위 %I64d이(가) 아닌 %I64d에 속합니다.|  
  
## <a name="explanation"></a>설명  
이 오류는 일반적으로 지정한 데이터베이스의 페이지 또는 할당이 손상되었음을 나타냅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 페이지 링크를 따라가거나 IAM(Index Allocation Map)을 사용하여 테이블에 속하는 페이지를 읽을 때 손상을 감지합니다. 테이블에 할당된 모든 페이지는 해당 테이블과 연결된 할당 단위 중 하나에 속해야 합니다. 페이지 머리글에 포함된 할당 단위 ID가 테이블에 연결된 할당 단위 ID와 일치하지 않으면 예외가 발생합니다. 오류 메시지에 나열된 첫 번째 할당 단위 ID는 페이지 머리글에 있는 ID이고 두 번째 할당 단위 값은 테이블과 연결된 ID입니다.  
  
**데이터 손상 오류**  
  
심각도 수준 21은 잠재적 데이터 손상을 나타냅니다. 가능한 원인은 손상된 페이지 체인, 손상된 IAM 또는 해당 개체에 대한 [sys.objects](~/relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰의 잘못된 항목입니다. 이러한 오류는 하드웨어 또는 디스크 장치 드라이버 오류로 인해 발생하는 경우가 많습니다.  
  
**일시적 오류**  
  
심각도 수준 12는 잠재적인 일시적 오류를 나타냅니다. 이 오류는 캐시에서 발생하며 디스크에 있는 데이터 손상을 나타내지 않습니다. 일시적 605 오류는 다음과 같은 조건에서 발생할 수 있습니다.  
  
-   운영 체제에서 I/O 작업이 완료되었다고 너무 빨리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 알리는 경우. 실제 데이터 손상이 없는 경우에도 오류 메시지가 표시됩니다.  
  
최적화 프로그램 힌트 NOLOCK을 사용하여 쿼리를 실행하거나 트랜잭션 격리 수준을 READ UNCOMMITTED로 설정하는 경우. NOLOCK 또는 READ UNCOMMITTED를 사용하는 쿼리에서 다른 사용자가 이동하거나 변경 중인 데이터를 읽으려고 하면 605 오류가 발생합니다. 일시적 605 오류인지 확인하려면 나중에 쿼리를 다시 실행합니다. 자세한 내용은 기술 자료 문서 [235880](http://support.microsoft.com/kb/235880/en-us) "You receive an "Error 605" error message when you run a query with the optimizer hint NOLOCK or you set the transaction isolation level to READ UNCOMMITTED in SQL Server."("SQL Server에서 최적화 프로그램 힌트 NOLOCK를 사용하여 쿼리를 실행하거나 트랜잭션 격리 수준을 READ UNCOMMITTED로 설정하면 "오류 605" 오류 메시지가 나타난다")를 참조하세요.  
  
일반적으로 데이터에 액세스하는 동안 오류가 발생했는데 후속 DBCC CHECKDB 작업이 오류 없이 완료되면 일시적 605 오류일 가능성이 큽니다.  
  
## <a name="user-action"></a>사용자 동작  
605 오류가 일시적 오류가 아니면 문제가 심각하며 다음 태스크를 수행하여 문제를 수정해야 합니다.  
  
1.  다음 쿼리를 실행하여 메시지에 지정된 할당 단위와 연결된 테이블을 식별합니다. `allocation_unit_id`를 오류 메시지에 지정된 할당 단위로 바꾸십시오.  
  
    USE`database_name`;  
  
    GO  
  
    SELECT au.allocation_unit_id, OBJECT_NAME(p.object_id) AS table_name, fg.name AS filegroup_name,  
  
    au.type_desc AS allocation_type, au.data_pages, partition_number  
  
    FROM sys.allocation_units AS au  
  
    JOIN sys.partitions AS p ON au.container_id = p.partition_id  
  
    JOIN sys.filegroups AS fg ON fg.data_space_id = au.data_space_id  
  
    WHERE au.allocation_unit_id = `allocation_unit_id` OR au.allocation_unit_id = `allocation_unit_id`  
  
    ORDER BY au.allocation_unit_id;  
  
    GO  
  
2.  오류 메시지에 지정된 두 번째 할당 단위 ID와 연결된 테이블에 대해 REPAIR 절 없이 DBCC CHECKTABLE을 실행합니다.  
  
3.  가능한 한 즉시 REPAIR 절 없이 DBCC CHECKDB를 실행하여 전체 데이터베이스의 전체 손상 범위를 확인합니다.  
  
4.  오류 로그에서 자주 605 오류와 함께 나타나는 다른 오류를 확인하고 Windows 이벤트 로그에서 시스템 또는 하드웨어 관련 문제를 확인합니다. 로그에 하드웨어 관련 문제가 포함되어 있으면 이를 해결하십시오.  
  
하드웨어 관련 문제가 아니면 다음 태스크 중 하나를 수행하십시오.  
  
1.  정상적인 백업을 사용하여 데이터베이스를 복원합니다. 페이지 복원 백업 기능을 사용하여 손상된 페이지만 복원할 수 있습니다.  
  
2.  3단계에서 수행한 DBCC CHECKDB 작업에서 권장하는 REPAIR 절을 사용하여 DBCC CHECKDB를 실행하고 손상을 복구합니다. REPAIR 절 중 하나를 사용하여 DBCC CHECKDB를 실행해도 문제가 해결되지 않으면 주 지원 공급자에게 문의하세요. DBCC CHECKDB의 출력을 검토할 수 있도록 제공하십시오.  
  
    > [!CAUTION]  
    > REPAIR 절을 사용할 경우 DBCC CHECKDB가 데이터에 미치는 영향을 확인하려면 이 문을 실행하기 전에 주 지원 공급자에게 문의하세요.  
  
## <a name="see-also"></a>참고 항목  
[DBCC CHECKTABLE&#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
  
