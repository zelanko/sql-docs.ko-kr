---
title: sys. dm_exec_cursors (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cursors_TSQL
- dm_exec_cursors
- dm_exec_cursors_TSQL
- sys.dm_exec_cursors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cursors dynamic management function
ms.assetid: f520b63c-36af-40f1-bf71-6901d6331d3d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f2482e9af7451463c03bb5deb2e63c7261ec5361
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882038"
---
# <a name="sysdm_exec_cursors-transact-sql"></a>sys.dm_exec_cursors(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  다양한 데이터베이스에서 열려 있는 커서에 대한 정보를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
dm_exec_cursors (session_id | 0 )  
```  
  
## <a name="arguments"></a>인수  
 *session_id* | 0  
 세션의 ID입니다. *Session_id* 지정 된 경우이 함수는 지정 된 세션의 커서에 대 한 정보를 반환 합니다.  
  
 0을 지정하면 모든 세션의 모든 커서에 대한 정보가 반환됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|이 커서를 보유하는 세션의 ID입니다.|  
|**cursor_id**|**int**|커서 개체의 ID입니다.|  
|**name**|**nvarchar(256)**|사용자가 정의한 커서의 이름입니다.|  
|**properties**|**nvarchar(256)**|커서의 속성을 지정합니다. 다음 속성의 값은 이 열의 값을 구성하도록 연결됩니다.<br />선언 인터페이스<br />커서 유형 <br />커서 동시성<br />커서 범위<br />커서 중첩 수준<br /><br /> 예를 들어이 열에 반환 된 값은 "TSQL &#124; Dynamic &#124; 낙관적 &#124; Global (0)" 일 수 있습니다.|  
|**sql_handle**|**varbinary(64)**|커서를 선언한 일괄 처리의 텍스트에 대한 핸들입니다.|  
|**statement_start_offset**|**int**|현재 실행 중인 일괄 처리 또는 저장 프로시저에서 현재 실행 중인 문이 시작되는 위치까지의 문자 수입니다. **Sql_handle**, **statement_end_offset**및 [dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) 동적 관리 함수와 함께 사용 하 여 요청에 대해 현재 실행 중인 문을 검색할 수 있습니다.|  
|**statement_end_offset**|**int**|현재 실행 중인 일괄 처리 또는 저장 프로시저에서 현재 실행 중인 문이 종료되는 위치까지의 문자 수입니다. **Sql_handle**, **statement_start_offset**및 **dm_exec_sql_text** 동적 관리 함수와 함께 사용 하 여 요청에 대해 현재 실행 중인 문을 검색할 수 있습니다.|  
|**plan_generation_num**|**bigint**|다시 컴파일한 후 계획의 인스턴스 간을 서로 구별하는 데 사용될 수 있는 시퀀스 번호입니다.|  
|**creation_time**|**datetime**|이 커서가 생성되었을 때의 타임스탬프입니다.|  
|**is_open**|**bit**|커서가 열려 있는지 여부를 지정합니다.|  
|**is_async_population**|**bit**|백그라운드 스레드가 여전히 KEYSET 또는 STATIC 커서를 비동기적으로 채우고 있는지 여부를 지정합니다.|  
|**is_close_on_commit**|**bit**|커서가 CURSOR_CLOSE_ON_COMMIT을 사용하여 선언되었는지 여부를 지정합니다.<br /><br /> 1 = 트랜잭션이 종료될 때 커서가 닫힙니다.|  
|**fetch_status**|**int**|커서의 마지막 인출 상태를 반환합니다. 마지막으로 반환 된 @ @FETCH_STATUS 값입니다.|  
|**fetch_buffer_size**|**int**|인출 버퍼 크기에 대한 정보를 반환합니다.<br /><br /> 1 = Transact-SQL 커서입니다. API 커서의 경우 더 높은 값으로 설정할 수 있습니다.|  
|**fetch_buffer_start**|**int**|FAST_FORWARD 및 DYNAMIC 커서의 경우, 커서가 열려 있지 않거나 첫 번째 행 앞에 있으면 0을 반환합니다. 그렇지 않으면 -1을 반환합니다.<br /><br /> STATIC 및 KEYSET 커서의 경우, 커서가 열려 있지 않으면 0을 반환하고 커서가 마지막 행 뒤에 있으면 -1을 반환합니다.<br /><br /> 그렇지 않으면 커서가 있는 행 번호를 반환합니다.|  
|**ansi_position**|**int**|인출 버퍼 내의 커서 위치입니다.|  
|**worker_time**|**bigint**|이 커서를 실행하는 작업자가 사용한 시간(마이크로초)입니다.|  
|**reads**|**bigint**|커서에 의해 수행된 읽기 수입니다.|  
|**writes**|**bigint**|커서에 의해 수행된 쓰기 수입니다.|  
|**dormant_duration**|**bigint**|이 커서에 대한 마지막 쿼리(열기 또는 인출)가 시작된 이후 경과한 시간(밀리초)입니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 다음 표에서는 커서 선언 인터페이스에 대한 정보를 제공하고 속성 열에 나올 수 있는 값을 보여 줍니다.  
  
|속성|설명|  
|--------------|-----------------|  
|API|데이터 액세스 API(ODBC, OLEDB) 중 하나를 사용하여 커서가 선언되었습니다.|  
|TSQL|Transact-SQL DECLARE CURSOR 구문을 사용하여 커서가 선언되었습니다.|  
  
 다음 표에서는 커서 유형에 대한 정보를 제공하고 속성 열에 나올 수 있는 값을 보여 줍니다.  
  
|형식|설명|  
|----------|-----------------|  
|Keyset|키 집합 커서로 선언되었습니다.|  
|동적|동적 커서로 선언되었습니다.|  
|스냅샷|스냅샷 또는 정적 커서로 선언되었습니다.|  
|Fast_Forward|빠른 정방향 커서로 선언되었습니다.|  
  
 다음 표에서는 커서 동시성에 대한 정보를 제공하고 속성 열에 나올 수 있는 값을 보여 줍니다.  
  
|동시성|설명|  
|-----------------|-----------------|  
|읽기 전용|커서가 읽기 전용으로 선언되었습니다.|  
|Scroll Locks|커서가 스크롤 잠금을 사용합니다.|  
|Optimistic|커서가 낙관적 동시성 제어를 사용합니다.|  
  
 다음 표에서는 커서 범위에 대한 정보를 제공하고 속성 열에 나올 수 있는 값을 보여 줍니다.  
  
|범위|Description|  
|-----------|-----------------|  
|로컬|커서 범위를 커서가 생성된 일괄 처리, 저장 프로시저, 트리거에 대해 로컬로 지정합니다.|  
|전역|커서 범위를 연결에 대해 전역으로 지정합니다.|  
  
## <a name="examples"></a>예  
  
### <a name="a-detecting-old-cursors"></a>A. 오래된 커서 검색  
 다음 예에서는 지정한 36시간을 초과하여 서버에서 열려 있는 커서에 대한 정보를 반환합니다.  
  
```  
SELECT creation_time, cursor_id, name, c.session_id, login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s ON c.session_id = s.session_id   
WHERE DATEDIFF(hh, c.creation_time, GETDATE()) > 36;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;관련 동적 관리 뷰 및 함수 실행](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
  

