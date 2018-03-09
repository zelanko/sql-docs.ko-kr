---
title: sp_describe_cursor (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- sp_describe_cursor
- sp_describe_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor
ms.assetid: 0c836c99-1147-441e-998c-f0a30cd05275
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38eae1442b8058b6596efd525196f2f76b4b6dce
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spdescribecursor-transact-sql"></a>sp_describe_cursor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 커서의 특성을 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_describe_cursor [ @cursor_return = ] output_cursor_variable OUTPUT   
     { [ , [ @cursor_source = ] N'local'  
    , [ @cursor_identity = ] N'local_cursor_name' ]   
   | [ , [ @cursor_source = ] N'global'  
    , [ @cursor_identity = ] N'global_cursor_name' ]   
   | [ , [ @cursor_source = ] N'variable'  
     , [ @cursor_identity = ] N'input_cursor_variable' ]   
     }   
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ @cursor_return=] *output_cursor_variable* 출력  
 커서 출력을 수신하기 위해 선언된 커서 변수의 이름입니다. *output_cursor_variable* 은 **커서**은 없으며 기본적으로, 또한 sp_describe_cursor가 호출 시 모든 커서와도 연결 수 없습니다. 반환된 커서는 스크롤할 수 있으며 동적인 읽기 전용 커서입니다.  
  
 [ @cursor_source=] {N'local' | N'global' | N'variable'을 (를)  
 보고할 커서를 로컬 커서, 전역 커서 또는 커서 변수의 이름 중 어느 것을 사용하여 지정할지 결정합니다. 매개 변수는 **nvarchar (30)**합니다.  
  
 [ @cursor_identity=] N'*local_cursor_name*']  
 LOCAL 키워드를 갖거나 LOCAL이 기본값인 DECLARE CURSOR 문에 의해 생성된 커서의 이름입니다. *local_cursor_name* 은 **nvarchar (128)**합니다.  
  
 [ @cursor_identity=] N'*global_cursor_name*']  
 GLOBAL 키워드를 갖거나 GLOBAL이 기본값인 DECLARE CURSOR 문에 의해 생성된 커서의 이름입니다. *global_cursor_name* 은 **nvarchar (128)**합니다.  
  
 *global_cursor_name* 그 다음 명명 된 ODBC 응용 프로그램에서 연 API 서버 커서의 이름일 수도 있습니다 SQLSetCursorName를 호출 하 여 합니다.  
  
 [ @cursor_identity=] N'*input_cursor_variable*']  
 열린 커서와 연관된 커서 변수의 이름입니다. *input_cursor_variable* 은 **nvarchar (128)**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="cursors-returned"></a>반환되는 커서  
 sp_describe_cursor는 결과 집합을 캡슐화는 [!INCLUDE[tsql](../../includes/tsql-md.md)] **커서** 출력 매개 변수입니다. 이로 인해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리, 저장 프로시저 및 한 번에 하나의 행만 출력 작업을 하는 트리거가 허용됩니다. 이는 데이터베이스 API 함수에서 바로 프로시저를 호출할 수 없음을 의미하기도 합니다. **커서** 출력 매개 변수를 프로그램 변수에 바인딩되어야 하지만 데이터베이스 Api는 바인딩을 지원 하지 않는 **커서** 매개 변수 또는 변수입니다.  
  
 다음 표에서는 sp_describe_cursor를 사용하여 반환된 커서의 형식을 보여 줍니다. 커서의 형식은 sp_cursor_list를 사용하여 반환되는 형식과 같습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|커서를 지칭할 때 사용하는 이름입니다. DECLARE CURSOR 문에서 지정한 이름으로 커서를 참조하는 경우 참조 이름과 커서 이름이 동일합니다. 변수로 커서를 참조하는 경우 변수 이름이 참조 이름이 됩니다.|  
|cursor_name|**sysname**|DECLARE CURSOR 문에서 지정된 커서 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 커서 변수를 커서로 설정하여 커서를 만든 경우 cursor_name은 커서 변수의 이름을 반환합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 출력 열은 시스템 생성 이름을 반환합니다.|  
|cursor_scope|**tinyint**|1 = 로컬<br /><br /> 2 = 전역|  
|상태|**int**|CURSOR_STATUS 시스템 함수가 보고한 것과 동일한 값입니다.<br /><br /> 1 = 커서 이름 또는 변수에 의해 참조되는 커서가 열려 있습니다. 커서가 변경 내용을 감지하지 않거나 정적이거나 키 집합인 경우 적어도 한 개 이상의 행이 있습니다. 커서가 동적인 경우 결과 집합에는 0개 이상의 행이 있습니다.<br /><br /> 0 = 커서 이름 또는 변수에 의해 참조되는 커서가 열려 있으나 행이 없습니다. 동적 커서는 이 값을 반환하지 않습니다.<br /><br /> -1 = 커서 이름 또는 변수에 의해 참조되는 커서가 닫혀 있습니다.<br /><br /> -2 = 커서 변수에만 적용됩니다. 변수에 할당된 커서가 없습니다. OUTPUT 매개 변수가 커서를 변수에 할당했으나 저장 프로시저가 반환 전에 커서를 닫았을 수 있습니다.<br /><br /> -3 = 지정된 이름의 커서 또는 커서 변수가 없거나 커서 변수에 할당된 커서가 없습니다.|  
|model|**tinyint**|1 = 변경 내용 미감지(또는 정적)<br /><br /> 2 = 키 집합<br /><br /> 3 = 동적<br /><br /> 4 = 빠른 전진|  
|동시성|**tinyint**|1 = 읽기 전용<br /><br /> 2 = 스크롤 잠금<br /><br /> 3 = 낙관적|  
|scrollable|**tinyint**|0 = 전진 전용<br /><br /> 1 = 스크롤 가능|  
|open_status|**tinyint**|0 = 닫힘<br /><br /> 1 = 열림|  
|cursor_rows|**decimal(10,0)**|결과 집합에서 한정하는 행 수입니다. 자세한 내용은 참조 [@@CURSOR_ROWS &#40; Transact SQL &#41; ](../../t-sql/functions/cursor-rows-transact-sql.md).|  
|fetch_status|**smallint**|해당 커서의 마지막 인출 상태입니다. 자세한 내용은 참조 [@@FETCH_STATUS &#40; Transact SQL &#41; ](../../t-sql/functions/fetch-status-transact-sql.md).<br /><br /> 0 = 인출 성공입니다.<br /><br /> -1 = 인출이 실패하였거나 커서의 범위 밖입니다.<br /><br /> -2 = 요청된 행이 누락되었습니다.<br /><br /> -9 = 커서에 대한 인출이 없습니다.|  
|column_count|**smallint**|커서 결과 집합 내의 열 수입니다.|  
|row_count|**decimal(10,0)**|커서의 마지막 작업에 의해 영향을 받는 행 수입니다. 자세한 내용은 참조 [@@ROWCOUNT &#40; Transact SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).|  
|last_operation|**tinyint**|커서에서 수행된 마지막 작업입니다.<br /><br /> 0 = 커서에서 작업이 수행되지 않았습니다.<br /><br /> 1 = 열기<br /><br /> 2 = 인출<br /><br /> 3 = 삽입<br /><br /> 4 = 업데이트<br /><br /> 5 = 삭제<br /><br /> 6 = 닫기<br /><br /> 7 = 할당 취소|  
|cursor_handle|**int**|서버 범위에서 고유한 커서의 값입니다.|  
  
## <a name="remarks"></a>주의  
 sp_describe_cursor는 스크롤 및 업데이트 허용 여부 등과 같은 서버 커서에 대한 전역 특성을 설명합니다. 커서가 반환한 결과 집합의 특성 설명을 보려면 sp_describe_cursor_columns를 사용하십시오. 커서가 참조하는 기본 테이블의 보고서를 보려면 sp_describe_cursor_tables를 사용하십시오. 연결 시 표시될 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서의 보고서를 얻으려면 sp_cursor_list를 사용하십시오.  
  
 DECLARE CURSOR 문에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 DECLARE CURSOR에 포함된 SELECT 문으로 지원할 수 없는 커서 유형을 요청하는 경우가 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 SELECT 문을 사용하여 커서를 지원할 수 있는 형식으로 암시적으로 변환합니다. DECLARE CURSOR 문에 TYPE_WARNING이 지정된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 응용 프로그램에 변환이 완료되었다는 정보 메시지를 전송합니다. sp_describe_cursor 구현 된 커서의 유형을 결정 하도록 호출할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 전역 커서를 열고 `sp_describe_cursor`를 사용하여 커서의 특성에 대해 보고합니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR STATIC FOR  
SELECT LastName  
FROM Person.Person;  
  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor into the cursor variable.  
EXEC master.dbo.sp_describe_cursor @cursor_return = @Report OUTPUT,  
        @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [커서](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40; Transact SQL &#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_cursor_list &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor_columns &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [sp_describe_cursor_tables &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
  
