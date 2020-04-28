---
title: sp_help_fulltext_tables (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables
- sp_help_fulltext_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables
ms.assetid: 86e24a5f-a869-43f6-b83e-c52b7b01b5ff
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4ac8e09eff53c04377ccd48a47cc31d9d7ddc5e8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68055017"
---
# <a name="sp_help_fulltext_tables-transact-sql"></a>sp_help_fulltext_tables(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  전체 텍스트 인덱싱용으로 등록된 테이블의 목록을 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 **fulltext_indexes** 카탈로그 뷰를 사용 하십시오. 자세한 내용은 [fulltext_indexes &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)을 참조 하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_tables [ [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'`전체 텍스트 카탈로그의 이름입니다. *fulltext_catalog_name* 는 **sysname**이며 기본값은 NULL입니다. *Fulltext_catalog_name* 를 생략 하거나 NULL 인 경우 데이터베이스와 연결 된 전체 텍스트 인덱싱된 테이블이 모두 반환 됩니다. *Fulltext_catalog_name* 지정 되었지만 *TABLE_NAME* 생략 되거나 NULL 인 경우이 카탈로그와 연결 된 모든 전체 텍스트 인덱싱된 테이블에 대해 전체 텍스트 인덱스 정보가 검색 됩니다. *Fulltext_catalog_name* 와 *table_name* 를 모두 지정 하는 경우 *table_name* *fulltext_catalog_name*와 연결 된 경우 행이 반환 됩니다. 그렇지 않으면 오류가 발생 합니다.  
  
`[ @table_name = ] 'table_name'`전체 텍스트 메타 데이터를 요청 하는 한 부분 또는 두 부분으로 구성 된 테이블 이름입니다. *table_name* 은 **nvarchar (517)** 이며 기본값은 NULL입니다. *Table_name* 만 지정 하면 *table_name* 관련 된 행만 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|테이블 소유자입니다. 테이블을 만든 데이터베이스 사용자의 이름입니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다.|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|고유한 키 열로 지정된 열에 UNIQUE 제약 조건을 부과하는 인덱스입니다.|  
|**FULLTEXT_KEY_COLID**|**int**|FULLTEXT_KEY_NAME에 의해 식별되는 고유한 인덱스의 열 ID입니다.|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|해당 테이블의 전체 텍스트 인덱싱에 대해 표시된 열이 쿼리에 적합한지 여부를 지정합니다.<br /><br /> 0 = 비활성<br /><br /> 1 = 활성|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|전체 텍스트 인덱스 데이터가 있는 전체 텍스트 카탈로그입니다.|  
  
## <a name="permissions"></a>사용 권한  
 실행 권한은 기본적으로 **public** 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Cat_Desc` 전체 텍스트 카탈로그에 연결된 전체 텍스트 인덱싱된 테이블의 이름을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_tables 'Cat_Desc';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [INDEXPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Transact-sql&#41;sp_fulltext_table &#40;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [Transact-sql&#41;sp_help_fulltext_tables_cursor &#40;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
