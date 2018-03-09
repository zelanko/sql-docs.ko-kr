---
title: sp_cursor_list (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_list
- sp_cursor_list_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_list
ms.assetid: 7187cfbe-d4d9-4cfa-a3bb-96a544c7c883
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b4ce00bf096ecbd0c40b723c017b21d6fa982d1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spcursorlist-transact-sql"></a>sp_cursor_list(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 연결에 대해 열려 있는 서버 커서의 특성을 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cursor_list [ @cursor_return = ] cursor_variable_name OUTPUT   
     , [ @cursor_scope = ] cursor_scope  
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ @cursor_return=] *cursor_variable_name*출력  
 선언된 커서 변수의 이름입니다. *cursor_variable_name* 은 **커서**, 기본값은 없습니다. 커서는 스크롤할 수 있으며 동적이고 읽기 전용입니다.  
  
 [ @cursor_scope=] *cursor_scope*  
 보고할 커서 수준을 지정합니다. *cursor_scope* 은 **int**이며 기본값은 없고 수 있습니다 이러한 값 중 하나 여야 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|1.|모든 로컬 커서를 보고합니다.|  
|2|모든 전역 커서를 보고합니다.|  
|3|로컬과 전역 커서 모두를 보고합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="cursors-returned"></a>반환되는 커서  
 sp_cursor_list는 결과 집합이 아니라 [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서 출력 매개 변수를 반환합니다. 따라서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리, 저장 프로시저 및 트리거가 한 번에 하나의 출력 행을 처리할 수 있습니다. 이는 데이터베이스 API 함수에서 직접 프로시저를 호출할 수 없음을 의미하기도 합니다. cursor 출력 매개 변수는 반드시 프로그램 변수에 바인딩되어야 하지만 데이터베이스 API는 cursor 매개 변수 또는 변수의 바인딩을 지원하지 않기 때문입니다.  
  
 다음은 sp_cursor_list에 의해 반환되는 커서의 형식입니다. 이 형식은 sp_describe_cursor에 의해 반환되는 커서 형식과 동일합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|커서를 참조할 때 사용하는 이름입니다. DECLARE CURSOR 문에서 지정된 이름으로 커서를 참조하는 경우 참조 이름과 커서 이름이 동일합니다. 커서에 대한 참조가 변수를 통해 이루어지는 경우 참조 이름은 커서 변수의 이름이 됩니다.|  
|cursor_name|**sysname**|DECLARE CURSOR 문의 커서 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]커서 변수를 커서로 설정 하 여 커서를 만든 경우 **cursor_name** 은 커서 변수의 이름을 반환 합니다.  이전 릴리스의 경우 이 출력 열은 시스템에서 생성한 이름을 반환합니다.|  
|cursor_scope|**smallint**|1 = 로컬<br /><br /> 2 = 전역|  
|상태|**smallint**|CURSOR_STATUS 시스템 함수에 의해 보고된 것과 동일한 값입니다.<br /><br /> 1 = 커서 이름 또는 변수에 의해 참조되는 커서가 열려 있습니다. 커서가 변경 내용을 감지하지 않거나 정적이거나 키 집합인 경우 적어도 한 개 이상의 행이 있습니다. 커서가 동적인 경우 결과 집합에는 0개 이상의 행이 있습니다.<br /><br /> 0 = 커서 이름 또는 변수에 의해 참조되는 커서가 열려 있으나 행이 없습니다. 동적 커서는 이 값을 반환하지 않습니다.<br /><br /> -1 = 커서 이름 또는 변수에 의해 참조되는 커서가 닫혀 있습니다.<br /><br /> -2 = 커서 변수에만 적용됩니다. 변수에 할당된 커서가 없습니다. OUTPUT 매개 변수가 커서를 변수에 할당했으나 저장 프로시저가 반환 전에 커서를 닫았을 수 있습니다.<br /><br /> -3 = 지정된 이름의 커서 또는 커서 변수가 없거나 커서 변수에 할당된 커서가 없습니다.|  
|model|**smallint**|1 = 변경 내용 미감지(또는 정적)<br /><br /> 2 = 키 집합<br /><br /> 3 = 동적<br /><br /> 4 = 빠른 전진|  
|동시성|**smallint**|1 = 읽기 전용<br /><br /> 2 = 스크롤 잠금<br /><br /> 3 = 낙관적|  
|scrollable|**smallint**|0 = 전진 전용<br /><br /> 1 = 스크롤 가능|  
|open_status|**smallint**|0 = 닫힘<br /><br /> 1 = 열림|  
|cursor_rows|**int**|결과 집합의 행 수입니다. 자세한 내용은 참조 [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)합니다.|  
|fetch_status|**smallint**|해당 커서의 마지막 인출 상태입니다. 자세한 내용은 참조 [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md):<br /><br /> 0 = 인출 성공입니다.<br /><br /> -1 = 인출이 실패하였거나 커서의 범위 밖입니다.<br /><br /> -2 = 요청된 행이 누락되었습니다.<br /><br /> -9 = 커서에 대한 인출이 없습니다.|  
|column_count|**smallint**|커서 결과 집합 내의 열 수입니다.|  
|row_count|**smallint**|커서의 마지막 조작에 의해 영향을 받는 행의 수입니다. 자세한 내용은 참조 [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md)합니다.|  
|last_operation|**smallint**|커서에서 수행된 마지막 작업입니다.<br /><br /> 0 = 커서에서 작업이 수행되지 않았습니다.<br /><br /> 1 = 열기<br /><br /> 2 = 인출<br /><br /> 3 = 삽입<br /><br /> 4 = 업데이트<br /><br /> 5 = 삭제<br /><br /> 6 = 닫기<br /><br /> 7 = 할당 취소|  
|cursor_handle|**int**|서버 범위에서 커서를 식별하는 고유한 값입니다.|  
  
## <a name="remarks"></a>주의  
 sp_cursor_list는 연결에 의해 열린 현재 서버 커서의 목록을 작성하고 커서의 스크롤 가능 여부 및 업데이트 가능성 등과 같은 각 커서의 전역 특성을 설명합니다. sp_cursor_list에 의해 나열되는 커서는 다음과 같습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서  
  
-   커서 이름을 지정 하는 SQLSetCursorName 다음 라고 하는 ODBC 응용 프로그램에 의해 열린 API 서버 커서입니다.  
  
 커서가 반환한 결과 집합의 특성 설명을 보려면 sp_describe_cursor_columns를 사용하십시오. 커서가 참조하는 기본 테이블의 보고서를 보려면 sp_describe_cursor_tables를 사용하십시오. sp_describe_cursor는 sp_cursor_list와 하지만 지정된 된 커서에 대해서만 동일한 정보를 보고합니다.  
  
## <a name="permissions"></a>Permissions  
 실행 권한은 기본적으로 public 역할로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 전역 커서를 열고 `sp_cursor_list`를 사용하여 커서의 특성에 대해 보고합니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a keyset-driven cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_cursor_list.  
DECLARE @Report CURSOR;  
  
-- Execute sp_cursor_list into the cursor variable.  
EXEC master.dbo.sp_cursor_list @cursor_return = @Report OUTPUT,  
      @cursor_scope = 2;  
  
-- Fetch all the rows from the sp_cursor_list output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_cursor_list.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
