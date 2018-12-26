---
title: sys.fn_get_sql (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_sql
- sys.fn_get_sql_TSQL
- fn_get_sql_TSQL
- sys.fn_get_sql
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_sql function
- text [SQL Server], SQL handles
- sys.fn_get_sql function
- valid SQL handles [SQL Server]
- SQL handles
ms.assetid: d5fe49b5-0813-48f2-9efb-9187716b2fd4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: db1c1d36bb3cb831a2f744a77529939894fff27a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47842061"
---
# <a name="sysfngetsql-transact-sql"></a>sys.fn_get_sql(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 SQL 핸들에 대한 SQL 문의 텍스트를 반환합니다.  
  
> [!IMPORTANT]  
>  Microsoft SQL Server의 이후 버전에서는 이 기능이 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. sys.dm_exec_sql_text를 대신 사용하십시오. 자세한 내용은 [sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)합니다.  
  
 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_get_sql ( SqlHandle )  
```  
  
## <a name="arguments"></a>인수  
 *SqlHandle*  
 핸들 값입니다. *SqlHandle* 됩니다 **varbinary(64)** 기본값은 없습니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|dbid|**smallint**|데이터베이스 ID입니다. 임시 및 준비된 SQL 문의 경우 문이 컴파일된 데이터베이스의 ID입니다.|  
|objectid|**int**|데이터베이스 개체의 ID입니다. 임시 SQL 문의 경우 NULL입니다.|  
|number|**smallint**|프로시저가 그룹화된 경우 그룹의 번호를 나타냅니다.<br /><br /> 0  =  항목이 프로시저가 아닙니다.<br /><br /> NULL = 임시 SQL 문입니다.|  
|encrypted|**bit**|개체가 암호화되었는지 여부를 나타냅니다.<br /><br /> 0 = 암호화되지 않음<br /><br /> 1 = 암호화됨|  
|text|**text**|SQL 문의 텍스트입니다. 암호화된 개체의 경우 NULL입니다.|  
  
## <a name="remarks"></a>Remarks  
 Sql_handle 열에서 유효한 SQL 핸들을 가져올 수 있습니다 합니다 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) 동적 관리 뷰.  
  
 핸들을 전달 하는 더 이상에 있는지 캐시 fn_get_sq**l** 빈 결과 집합을 반환 합니다. 유효하지 않은 핸들을 전달하는 경우 일괄 처리가 중지되고 오류 메시지가 반환됩니다.  
  
 합니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 일부를 캐시할 수 없으며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 대량 복사 문과 문자열 리터럴이 8KB를 초과 하는 문 등의 문에서 합니다. 이러한 문에 대한 핸들은 fn_get_sql을 사용하여 검색할 수 없습니다.  
  
 합니다 **텍스트** 결과 집합의 열 암호를 포함할 수 있는 텍스트가 필터링 됩니다. 모니터링 되지 않은 자세한 저장 관련 보안에 대 한 정보 절차를 참조 [추적 필터링](../../relational-databases/sql-trace/filter-a-trace.md)합니다.  
  
 Fn_get_sql 함수와 비슷한 정보를 반환 합니다 [DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md) 명령입니다. 다음은 DBCC INPUTBUFFER를 사용할 수 없기 때문에 fn_get_sql 함수를 사용할 수 있는 경우의 예입니다.  
  
-   이벤트가 255자 이상을 포함할 경우  
  
-   저장 프로시저의 가장 높은 현재 중첩 수준을 반환해야 하는 경우. 예를 들어 sp_1과 sp_2라는 두 저장 프로시저가 있습니다. sp_1이 sp_2를 호출하고 sp_2가 실행되는 동안 사용자가 sys.dm_exec_requests 동적 관리 뷰에서 핸들을 가져오면 fn_get_sql 함수는 sp_2에 대한 정보를 반환합니다. 또한 fn_get_sql 함수는 가장 높은 현재 중첩 수준에 있는 저장 프로시저의 완전한 텍스트를 반환합니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 VIEW SERVER STATE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 데이터베이스 관리자는 다음 예에서처럼 fn_get_sql 함수를 사용하여 문제점 진단 프로세스에 도움을 줄 수 있습니다. 관리자는 문제점이 있는 세션 ID를 식별한 후에 해당 세션에 대한 SQL 핸들을 검색하고 해당 핸들을 사용하여 fn_get_sql 함수를 호출하고 시작 및 종료 오프셋을 사용하여 문제점이 있는 세션 ID의 SQL 텍스트를 확인할 수 있습니다.  
  
```  
DECLARE @Handle varbinary(64);  
SELECT @Handle = sql_handle   
FROM sys.dm_exec_requests   
WHERE session_id = 52 and request_id = 0;  
SELECT * FROM sys.fn_get_sql(@Handle);  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [DBCC INPUTBUFFER &#40;TRANSACT-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)   
 [sys.sysprocesses &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests&#40;Transact-SQL&#41](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
