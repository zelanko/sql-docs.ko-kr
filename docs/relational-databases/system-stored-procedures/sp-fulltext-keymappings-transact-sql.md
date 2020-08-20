---
description: sp_fulltext_keymappings(Transact-SQL)
title: sp_fulltext_keymappings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_keymappings_TSQL
- sp_fulltext_keymappings
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], key column
- sp_fulltext_keymappings
- full-text indexes [SQL Server], troubleshooting
ms.assetid: 2818fa42-072d-4664-a2f7-7ec363b51d81
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 59445fdd9d4d7588291b2fac0073b962155cde04
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464375"
---
# <a name="sp_fulltext_keymappings-transact-sql"></a>sp_fulltext_keymappings(Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  문서 ID(DocId)와 전체 텍스트 키 값 간의 매핑을 반환합니다. DocId 열에는 전체 텍스트 인덱싱된 테이블의 특정 전체 텍스트 키 값에 매핑되는 **bigint** 정수 값이 포함 됩니다. 검색 조건을 만족하는 DocId 값이 전체 텍스트 엔진에서 데이터베이스 엔진으로 전달되고 여기서 쿼리되는 기본 테이블의 전체 텍스트 키 값에 매핑됩니다. 전체 텍스트 키 열은 테이블의 특정 열에 필요한 고유 인덱스입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_fulltext_keymappings { table_id | table_id, docid | table_id, NULL, key }  
```  
  
#### <a name="parameters"></a>매개 변수  
 *table_id*  
 전체 텍스트 인덱싱된 테이블의 개체 ID입니다. 잘못 된 *table_id*를 지정 하면 오류가 반환 됩니다. 테이블의 개체 ID를 가져오는 방법에 대 한 자세한 내용은 [OBJECT_ID &#40;transact-sql&#41;](../../t-sql/functions/object-id-transact-sql.md)을 참조 하십시오.  
  
 *docid*  
 키 값에 해당하는 내부 문서 ID(DocId)입니다. 잘못된 *docid* 값은 결과를 반환하지 않습니다.  
  
 *key*  
 지정한 테이블의 전체 텍스트 키 값입니다. 잘못된 *key* 값은 결과를 반환하지 않습니다. 전체 텍스트 키 값에 대 한 자세한 내용은 [전체 텍스트 인덱스 관리](https://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1)를 참조 하세요.  
  
> [!IMPORTANT]  
>  한 개, 두 개 또는 세 개의 매개 변수를 사용하는 방법은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|DocId|**bigint**|키 값에 해당하는 내부 문서 ID(DocId) 열입니다.|  
|키|*|지정한 테이블의 전체 텍스트 키 값입니다.<br /><br /> 매핑 테이블에 전체 텍스트 키가 없으면 빈 행 집합이 반환됩니다.|  
  
 <sup>*</sup> Key의 데이터 형식은 기본 테이블에 있는 전체 텍스트 키 열의 데이터 형식과 동일 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 함수는 공개 함수이며 특별한 사용 권한이 필요하지 않습니다.  
  
## <a name="remarks"></a>설명  
 다음 표에서는 한 개, 두 개 또는 세 개의 매개 변수를 사용한 결과에 대해 설명합니다.  
  
|이 매개 변수 목록 ...|다음 결과가 발생 했습니다.|  
|--------------------------|----------------------|  
|*table_id*|*Table_id* 매개 변수만 사용 하 여 호출 하는 경우 sp_fulltext_keymappings는 지정 된 기본 테이블의 모든 전체 텍스트 키 (키) 값과 각 키에 해당 하는 DocId를 반환 합니다. 여기에는 삭제가 보류된 키가 포함됩니다.<br /><br /> 이 함수는 다양한 문제를 해결하는 데 유용합니다. 특히, 선택한 전체 텍스트 키가 정수 데이터 형식이 아닐 경우 전체 텍스트 인덱스 내용을 보는 데 유용합니다. 여기에는 sp_fulltext_keymappings의 결과를 **sys. dm_fts_index_keywords_by_document**의 결과와 조인 하는 작업이 포함 됩니다. 자세한 내용은 [dm_fts_index_keywords_by_document &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)을 참조 하십시오.<br /><br /> 그러나 일반적으로는 가능하면 sp_fulltext_keymappings를 특정 전체 텍스트 키나 DocId를 지정하는 매개 변수와 함께 실행하는 것이 좋습니다. 이 방법은 전체 키 맵을 반환하는 것보다 훨씬 효율적입니다. 특히 매우 큰 테이블의 경우 전체 키 맵을 반환하기 위한 성능 비용이 상당히 크므로 더욱 효율적입니다.|  
|*table_id*, *docid*|*Table_id* 및 *docid* 만 지정 된 경우에는 *docid* 가 null이 아니어야 하 고 지정 된 테이블에 올바른 docid를 지정 해야 합니다. 이 함수는 특정 전체 텍스트 인덱스의 DocId에 해당하는 기본 테이블에서 사용자 지정 전체 텍스트 키를 분리하는 데 유용합니다.|  
|*table_id*, NULL, *키*|세 개의 매개 변수가 있는 경우 두 번째 매개 변수는 NULL 이어야 하 고 *키는* null이 아니어야 하며 지정 된 테이블에서 유효한 전체 텍스트 키 값을 지정 해야 합니다. 이 함수는 특정 전체 텍스트 키에 해당하는 DocId를 기본 테이블에서 분리하는 데 유용합니다.|  
  
 다음과 같은 경우 오류가 반환됩니다.  
  
-   잘못 된 *table_id*를 지정 합니다.  
  
-   테이블이 전체 텍스트 인덱싱되지 않은 경우  
  
-   NULL이 아닐 수 있는 매개 변수에 대해 NULL이 발생한 경우  
  
## <a name="examples"></a>예제  
  
> [!NOTE]  
>  이 섹션의 예에서는 `Production.ProductReview` 예제 데이터베이스의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 테이블을 사용합니다. `ProductReview` [Transact-sql&#41;&#40;전체 텍스트 인덱스 만들기 ](../../t-sql/statements/create-fulltext-index-transact-sql.md)에서 테이블에 대해 제공 된 예를 실행 하 여이 인덱스를 만들 수 있습니다.  
  
### <a name="a-obtaining-all-the-key-and-docid-values"></a>A. 모든 Key 및 DocId 값 가져오기  
 다음 예에서는 [DECLARE](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 문을 사용 하 여 지역 변수를 만들고 `@table_id` 테이블의 ID를 `ProductReview` 해당 값으로 할당 합니다. 이 예에서는 **sp_fulltext_keymappings** `@table_id` *table_id* 매개 변수에 대해를 지정 하 sp_fulltext_keymappings를 실행 합니다.  
  
> [!NOTE]  
>  *Table_id* 매개 변수만 **sp_fulltext_keymappings** 를 사용 하는 것은 작은 테이블에 적합 합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id;  
GO  
  
```  
  
 이 예에서는 다음과 같이 테이블에서 모든 DocId 및 전체 텍스트 키를 반환합니다.  
  
| TABLE | docid | key |
| ----- | ----- | --- |
|`1`|`1`|`1`|  
|`2`|`2`|`2`|  
|`3`|`3`|`3`|  
|`4`|`4`|`4`|  
  
### <a name="b-obtaining-the-docid-value-for-a-specific-key-value"></a>B. 특정 Key 값에 대한 DocId 값 가져오기  
 다음 예에서는 DECLARE 문을 사용하여 지역 변수 `@table_id`를 만들고 `ProductReview` 테이블의 ID를 해당 값으로 할당합니다. 이 예에서는 table_id 매개 변수에 대해를 지정 하 **sp_fulltext_keymappings** 를 실행 하 `@table_id` 고, *docid* 매개 변수에 NULL을 지정 하 고, *table_id* *키* 매개 변수에 대해 4를 실행 합니다.  
  
> [!NOTE]  
>  작은 테이블에 적합 한 *table_id* 매개 변수가 **sp_fulltext_keymappings** 사용 합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id, NULL, 4;  
GO  
  
```  
  
 이 예에서는 다음 결과를 반환합니다.  
  
| TABLE | docid | key |
| ----- | ----- | --- |
|`4`|`4`|`4`|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;전체 텍스트 검색 및 의미 체계 검색 저장 프로시저 ](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
