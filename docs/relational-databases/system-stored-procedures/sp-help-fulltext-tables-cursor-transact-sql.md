---
title: sp_help_fulltext_tables_cursor (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables_cursor
- sp_help_fulltext_tables_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables_cursor
ms.assetid: 155791eb-8832-4596-8487-7fc70dfba5b9
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0e188636c3152c6ba7e1daa941f01c5766ad4320
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpfulltexttablescursor-transact-sql"></a>sp_help_fulltext_tables_cursor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  커서를 사용하여 전체 텍스트 인덱싱에 등록된 테이블의 목록을 반환할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 새로운 **sys.fulltext_indexes** 카탈로그 뷰를 대신 합니다. 자세한 내용은 참조 [sys.fulltext_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_tables_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@cursor_return=** ] *@cursor_variable* 출력  
 유형의 출력 변수 **커서**합니다. 커서는 읽기 전용의 스크롤할 수 있는 동적 커서입니다.  
  
 [ **@fulltext_catalog_name=** ] **'***fulltext_catalog_name***'**  
 전체 텍스트 카탈로그의 이름입니다. *fulltext_catalog_name* 은 **sysname**, 기본값은 NULL입니다. 경우 *fulltext_catalog_name* 생략 되거나 null 인 경우 데이터베이스와 연관 된 모든 전체 텍스트 인덱싱된 테이블이 반환 됩니다. 경우 *fulltext_catalog_name* 를 지정 하지만 *table_name* 생략 되거나 null 인 경우이 카탈로그와 연결 된 모든 전체 텍스트 인덱싱된 테이블에 대 한 전체 텍스트 인덱스 정보가 검색 됩니다. 두 *fulltext_catalog_name* 및 *table_name* 를 지정 하는 경우 행이 반환 *table_name* 관련 된 *fulltext_catalog_name*; 그렇지 않으면 오류가 발생 합니다.  
  
 [ **@table_name=**] **'***table_name***'**  
 전체 텍스트 메타데이터를 요청한 대상이 되는 한 부분 또는 두 부분으로 구성된 테이블 이름입니다. *table_name* 은 **nvarchar (517)**, 기본값은 NULL입니다. 경우에 *table_name* 지정 된 행에만 관련이 *table_name* 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|테이블 소유자입니다. 테이블을 만든 데이터베이스 사용자의 이름입니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다.|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|고유한 키 열로 지정된 열에 UNIQUE 제약 조건을 부과하는 인덱스입니다.|  
|**FULLTEXT_KEY_COLID**|**int**|FULLTEXT_KEY_NAME에 의해 식별되는 고유한 인덱스의 열 ID입니다.|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|해당 테이블의 전체 텍스트 인덱싱에 대해 표시된 열이 쿼리에 적합한지 여부를 지정합니다.<br /><br /> 0 = 비활성<br /><br /> 1 = 활성|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|전체 텍스트 인덱스 데이터가 있는 전체 텍스트 카탈로그입니다.|  
  
## <a name="permissions"></a>Permissions  
 실행 권한은 기본적으로 **public** 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Cat_Desc` 전체 텍스트 카탈로그에 연결된 전체 텍스트 인덱싱된 테이블의 이름을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_tables_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>관련 항목:  
 [INDEXPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
