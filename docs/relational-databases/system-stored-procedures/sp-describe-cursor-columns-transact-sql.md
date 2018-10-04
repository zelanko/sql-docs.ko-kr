---
title: sp_describe_cursor_columns (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_columns
- sp_describe_cursor_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_columns
ms.assetid: 6eaa54af-7ba4-4fce-bf6c-6ac67cc1ac94
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c64e89fd5d965b98b59107d6047e6f43c0bcc9b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716711"
---
# <a name="spdescribecursorcolumns-transact-sql"></a>sp_describe_cursor_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 커서의 결과 집합에 있는 열의 특성을 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_describe_cursor_columns   
   [ @cursor_return = ] output_cursor_variable OUTPUT   
    { [ , [ @cursor_source = ] N'local' ,   
          [ @cursor_identity = ] N'local_cursor_name' ]   
    | [ , [ @cursor_source = ] N'global' ,   
          [ @cursor_identity = ] N'global_cursor_name' ]   
    | [ , [ @cursor_source = ] N'variable' ,   
          [ @cursor_identity = ] N'input_cursor_variable' ]   
   }  
```  
  
## <a name="arguments"></a>인수  
 [ @cursor_return=] *output_cursor_variable* 출력  
 커서 출력을 수신하기 위해 선언된 커서 변수의 이름입니다. *output_cursor_variable* 됩니다 **커서**없습니다 기본적 이며 반드시 sp_describe_cursor_columns가 호출 시 모든 커서와도 연결 수 없습니다. 반환된 커서는 스크롤할 수 있으며 동적인 읽기 전용 커서입니다.  
  
 [ @cursor_source=] {N'local' | N'global' | N'variable'}  
 보고할 커서를 로컬 커서, 전역 커서 또는 커서 변수의 이름 중 어느 것을 사용하여 지정할지 결정합니다. 매개 변수가 **nvarchar(30)** 합니다.  
  
 [ @cursor_identity=] N'*local_cursor_name*'  
 LOCAL 키워드를 갖거나 LOCAL이 기본값인 DECLARE CURSOR 문에 의해 생성된 커서의 이름입니다. *local_cursor_name* 됩니다 **nvarchar (128)** 합니다.  
  
 [ @cursor_identity=] N'*global_cursor_name*'  
 GLOBAL 키워드를 갖거나 GLOBAL이 기본값인 DECLARE CURSOR 문에 의해 생성된 커서의 이름입니다. *global_cursor_name* 됩니다 **nvarchar (128)** 합니다.  
  
 *global_cursor_name* 는 ODBC 응용 프로그램에서 열리고 다음 SQLSetCursorName를 호출 하 여 명명 된 API 서버 커서의 이름일 수도 있습니다.  
  
 [ @cursor_identity=] N'*input_cursor_variable*'  
 열린 커서와 연관된 커서 변수의 이름입니다. *input_cursor_variable* 됩니다 **nvarchar (128)** 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="cursors-returned"></a>반환되는 커서  
 sp_describe_cursor_columns는 해당 보고서를 캡슐화를 [!INCLUDE[tsql](../../includes/tsql-md.md)] **커서** 매개 변수를 출력 합니다. 이로 인해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리, 저장 프로시저 및 한 번에 하나의 행만 출력 작업을 하는 트리거가 허용됩니다. 이는 데이터베이스 API 함수에서 바로 프로시저를 호출할 수 없음을 의미하기도 합니다. 합니다 **커서** 출력 매개 변수를 프로그램 변수에 바인딩되어야 하지만 데이터베이스 Api는 바인딩을 지원 하지 않기 **커서** 매개 변수 또는 변수입니다.  
  
 다음 표에서는 sp_describe_cursor_columns를 사용할 때 반환되는 커서의 형식을 보여 줍니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|column_name|**sysname** (nullable)|결과 집합 열에 할당된 이름입니다. AS 절 없이 열이 지정된 경우에는 열이 NULL이 됩니다.|  
|ordinal_position|**int**|결과 집합의 제일 왼쪽에 있는 열에 대한 상대 위치입니다. 첫 번째 열은 0번 위치에 있습니다.|  
|column_characteristics_flags|**int**|OLE DB의 DBCOLUMNFLAGS에 저장된 정보를 표시하는 비트 마스크입니다. 다음과 같이 하나 또는 여러 개를 조합하여 지정할 수 있습니다.<br /><br /> 1 = 책갈피<br /><br /> 2 = 고정 길이<br /><br /> 4 = Null 허용<br /><br /> 8 = 행 버전 관리<br /><br /> 16 = 업데이트할 수 있는 열(FOR UPDATE 절이 없는 커서의 예상 열에 대해 설정하며 해당 열이 있는 경우 커서당 한 개씩만 사용할 수 있음)<br /><br /> 비트 값이 조합된 경우 조합된 비트 값의 특성이 적용됩니다. 예를 들어 비트 값이 6인 경우 열은 고정 길이(2), null 허용(4) 열이 됩니다.|  
|column_size|**int**|열의 값에 대한 최대 가능 크기입니다.|  
|data_type_sql|**smallint**|열의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 표시하는 번호입니다.|  
|column_precision|**tinyint**|기준으로 열의 최대 전체 자릿수는 *bPrecision* OLE DB의 값입니다.|  
|column_scale|**tinyint**|에 대 한 소수점 오른쪽 자릿수는 **숫자** 또는 **10 진수** 데이터 형식을 기준으로 합니다 *bScale* OLE DB의 값입니다.|  
|order_position|**int**|열이 결과 집합의 순서 지정에 참여한 경우 제일 왼쪽 열을 기준으로 했을 때 순서 키에 있는 열의 위치입니다.|  
|order_direction|**varchar(1)**(nullable)|A = 열이 순서 키에 있으며 오름차순입니다.<br /><br /> D = 열이 순서 키에 있으며 내림차순입니다.<br /><br /> NULL = 열이 순서 지정에 참여하지 않습니다.|  
|hidden_column|**smallint**|0 = 이 열이 선택 목록에 표시됩니다.<br /><br /> 1 = 나중에 사용하도록 예약되었습니다.|  
|columnid|**int**|기본 열의 열 ID입니다. 결과 집합 열이 식에서 작성된 경우 columnid는 -1입니다.|  
|objectid|**int**|열을 제공하는 개체 또는 주 테이블의 개체 ID입니다. 결과 집합 열이 식에서 작성된 경우 objectid는 -1입니다.|  
|dbid|**int**|열을 제공하는 기본 테이블을 포함한 데이터베이스의 ID입니다. 결과 집합 열이 식에서 작성된 경우 dbid는 -1입니다.|  
|dbname|**sysname**<br /><br /> (Null 허용)|열을 제공하는 기본 테이블을 포함한 데이터베이스의 이름입니다. 결과 집합 열이 식에서 작성된 경우 dbname은 NULL입니다.|  
  
## <a name="remarks"></a>Remarks  
 sp_describe_cursor_columns는 각 커서의 이름 및 데이터 형식 등 서버 커서의 결과 집합에 있는 열의 특성을 설명합니다. 서버 커서의 전역 특성을 설명을 보려면 sp_describe_cursor를 사용하십시오. 커서가 참조하는 기본 테이블의 보고서를 보려면 sp_describe_cursor_tables를 사용하십시오. 연결 시 표시될 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서의 보고서를 얻으려면 sp_cursor_list를 사용하십시오.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 전역 커서를 열고 `sp_describe_cursor_columns`를 사용하여 커서에 사용되는 열에 대해 보고합니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person;  
GO  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_columns.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_columns into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_columns  
    @cursor_return = @Report OUTPUT  
    ,@cursor_source = N'global'   
    ,@cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_columns output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_columns.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [커서](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40;TRANSACT-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_describe_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_cursor_list &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
