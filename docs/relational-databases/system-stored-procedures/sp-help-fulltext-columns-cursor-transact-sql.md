---
title: sp_help_fulltext_columns_cursor (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns_cursor
- sp_help_fulltext_columns_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns_cursor
ms.assetid: 26054e76-53b7-4004-8d48-92ba3435e9d7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6d158c0703190e78209c9a9550040f9bc667b371
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65983051"
---
# <a name="sphelpfulltextcolumnscursor-transact-sql"></a>sp_help_fulltext_columns_cursor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  커서를 사용하여 전체 텍스트 인덱싱에 등록된 열을 반환할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 된 [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) 카탈로그 뷰를 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_columns_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @cursor_return = ] @cursor_variable OUTPUT` 유형의 출력 변수 **커서**합니다. 결과 커서는 읽기 전용의 스크롤할 수 있는 동적 커서입니다.  
  
`[ @table_name = ] 'table_name'` 전체 텍스트 인덱스 정보를 요청한 대상 하나 또는 두 부분 구성 테이블 이름이입니다. *table_name* 됩니다 **nvarchar(517)** , 기본값은 NULL입니다. 하는 경우 *table_name* 를 생략 하면 모든 전체 텍스트 인덱싱된 테이블에 대 한 전체 텍스트 인덱스 열 정보가 검색 됩니다.  
  
`[ @column_name = ] 'column_name'` 전체 텍스트 인덱스 메타 데이터가 필요한 열의 이름이입니다. *column_name* 됩니다 **sysname** 이며 기본값은 NULL입니다. 하는 경우 *column_name* 이 생략 되거나 NULL에 대 한 전체 텍스트 인덱싱된 열 마다 전체 텍스트 열 정보가 반환 됩니다 *table_name*합니다. 하는 경우 *table_name* 생략 하거나 NULL 인 데이터베이스의 모든 테이블에 대 한 전체 텍스트 인덱싱된 열 마다 전체 텍스트 인덱스 열 정보가 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|테이블 소유자입니다. 테이블을 만든 데이터베이스 사용자의 이름입니다.|  
|**TABLE_ID**|**int**|테이블 ID입니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다.|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|인덱싱하기 위해 지정한 전체 텍스트 인덱싱된 테이블의 열입니다.|  
|**FULLTEXT_COLID**|**int**|전체 텍스트 인덱싱된 열의 ID입니다.|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|전체 텍스트 인덱싱된 열의 문서 유형을 지정하는 전체 텍스트 인덱싱된 테이블의 열입니다. 이 값은 전체 텍스트 인덱싱된 열 때 적용할 수만 **varbinary (max)** 하거나 **이미지** 열입니다.|  
|**FULLTEXT_BLOBTP_COLID**|**int**|문서 유형 열의 ID입니다. 이 값은 전체 텍스트 인덱싱된 열 때 적용할 수만 **varbinary (max)** 하거나 **이미지** 열입니다.|  
|**FULLTEXT_LANGUAGE**|**sysname**|열의 전체 텍스트 검색에 사용된 언어입니다.|  
  
## <a name="permissions"></a>사용 권한  
 실행 권한은 기본적으로 **public** 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스의 모든 테이블에서 전체 텍스트를 인덱싱하기 위해 지정된 열에 관한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_columns_cursor @mycursor OUTPUT  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>관련 항목  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
