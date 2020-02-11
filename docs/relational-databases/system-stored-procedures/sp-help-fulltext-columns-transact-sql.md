---
title: sp_help_fulltext_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns
- sp_help_fulltext_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns
ms.assetid: 92c8656b-f7fd-4904-9796-acc9ffed4106
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8009c9d2aa5f4b8f8be873633420bd1b088ece16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055095"
---
# <a name="sp_help_fulltext_columns-transact-sql"></a>sp_help_fulltext_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  전체 텍스트 인덱싱하기 위해 지정한 열을 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) 카탈로그 뷰를 사용 하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @table_name = ] 'table\_name'`전체 텍스트 인덱스 정보를 요청 하는 한 부분 또는 두 부분으로 구성 된 테이블 이름입니다. *table_name* 은 **nvarchar (517)** 이며 기본값은 NULL입니다. *Table_name* 를 생략 하면 전체 텍스트 인덱싱된 테이블 마다 전체 텍스트 인덱스 열 정보가 검색 됩니다.  
  
`[ @column_name = ] 'column\_name'`전체 텍스트 인덱스 메타 데이터를 요청한 열의 이름입니다. *column_name* 는 **sysname**이며 기본값은 NULL입니다. *Column_name* 생략 하거나 NULL 인 경우 *table_name*의 모든 전체 텍스트 인덱싱된 열에 대해 전체 텍스트 열 정보가 반환 됩니다. *Table_name* 도 생략 하거나 NULL 인 경우 데이터베이스의 모든 테이블에 대 한 전체 텍스트 인덱싱된 열 마다 전체 텍스트 인덱스 열 정보가 반환 됩니다.  
  
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
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|전체 텍스트 인덱싱된 열의 문서 유형을 지정하는 전체 텍스트 인덱싱된 테이블의 열입니다. 이 값은 전체 텍스트 인덱싱된 열이 **varbinary (max)** 또는 **image** 열인 경우에만 적용할 수 있습니다.|  
|**FULLTEXT_BLOBTP_COLID**|**int**|문서 유형 열의 ID입니다. 이 값은 전체 텍스트 인덱싱된 열이 **varbinary (max)** 또는 **image** 열인 경우에만 적용할 수 있습니다.|  
|**FULLTEXT_LANGUAGE**|**sysname**|열의 전체 텍스트 검색에 사용된 언어입니다.|  
  
## <a name="permissions"></a>사용 권한  
 실행 권한은 기본적으로 **public** 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Document` 테이블에서 전체 텍스트 인덱싱을 위해 지정된 열에 대한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_columns 'Production.Document';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [COLUMNPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [Transact-sql&#41;sp_fulltext_column &#40;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [Transact-sql&#41;sp_help_fulltext_columns_cursor &#40;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
