---
title: sp_help_fulltext_tables_cursor (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables_cursor
- sp_help_fulltext_tables_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables_cursor
ms.assetid: 155791eb-8832-4596-8487-7fc70dfba5b9
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 03636c70300b0a01a6f07d5d5fc3b9d0c4d6d506
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827682"
---
# <a name="sp_help_fulltext_tables_cursor-transact-sql"></a>sp_help_fulltext_tables_cursor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  커서를 사용하여 전체 텍스트 인덱싱에 등록된 테이블의 목록을 반환할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 새 **sys. fulltext_indexes** 카탈로그 뷰를 사용 하십시오. 자세한 내용은 [fulltext_indexes &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)을 참조 하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_tables_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @cursor_return = ] @cursor_variable OUTPUT`**Cursor**유형의 출력 변수입니다. 커서는 읽기 전용의 스크롤할 수 있는 동적 커서입니다.  
  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'`전체 텍스트 카탈로그의 이름입니다. *fulltext_catalog_name* 는 **sysname**이며 기본값은 NULL입니다. *Fulltext_catalog_name* 를 생략 하거나 NULL 인 경우 데이터베이스와 연결 된 전체 텍스트 인덱싱된 테이블이 모두 반환 됩니다. *Fulltext_catalog_name* 지정 되었지만 *TABLE_NAME* 생략 되거나 NULL 인 경우이 카탈로그와 연결 된 모든 전체 텍스트 인덱싱된 테이블에 대해 전체 텍스트 인덱스 정보가 검색 됩니다. *Fulltext_catalog_name* 와 *table_name* 를 모두 지정 하는 경우 *table_name* *fulltext_catalog_name*와 연결 된 경우 행이 반환 됩니다. 그렇지 않으면 오류가 발생 합니다.  
  
`[ @table_name = ] 'table_name'`전체 텍스트 메타 데이터를 요청 하는 한 부분 또는 두 부분으로 구성 된 테이블 이름입니다. *table_name* 은 **nvarchar (517)** 이며 기본값은 NULL입니다. *Table_name* 만 지정 하면 *table_name* 관련 된 행만 반환 됩니다.  
  
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
  
## <a name="permissions"></a>권한  
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
  
## <a name="see-also"></a>참고 항목  
 [INDEXPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Transact-sql&#41;sp_fulltext_table &#40;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [Transact-sql&#41;sp_help_fulltext_tables &#40;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
