---
title: sp_fulltext_keymappings (TRANSACT-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ef8bd6cfbcc10fa0625b4925da618ab275331a32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124239"
---
# <a name="spfulltextkeymappings-transact-sql"></a>sp_fulltext_keymappings(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  문서 ID(DocId)와 전체 텍스트 키 값 간의 매핑을 반환합니다. DocId 열에 대 한 값을 포함 한 **bigint** 전체 텍스트 인덱싱된 테이블의 특정 전체 텍스트 키 값에 매핑되는 정수입니다. 검색 조건을 만족하는 DocId 값이 전체 텍스트 엔진에서 데이터베이스 엔진으로 전달되고 여기서 쿼리되는 기본 테이블의 전체 텍스트 키 값에 매핑됩니다. 전체 텍스트 키 열은 테이블의 특정 열에 필요한 고유 인덱스입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_fulltext_keymappings { table_id | table_id, docid | table_id, NULL, key }  
```  
  
#### <a name="parameters"></a>매개 변수  
 *table_id*  
 전체 텍스트 인덱싱된 테이블의 개체 ID입니다. 잘못 된을 지정 하는 경우 *table_id*, 오류가 반환 됩니다. 테이블의 개체 ID를 얻는 방법에 대 한 자세한 내용은 [OBJECT_ID &#40;TRANSACT-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)합니다.  
  
 *docid*  
 키 값에 해당하는 내부 문서 ID(DocId)입니다. 잘못된 *docid* 값은 결과를 반환하지 않습니다.  
  
 *key*  
 지정한 테이블의 전체 텍스트 키 값입니다. 잘못된 *key* 값은 결과를 반환하지 않습니다. 전체 텍스트 키 값에 대 한 자세한 내용은 [전체 텍스트 인덱스 관리](https://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1)합니다.  
  
> [!IMPORTANT]  
>  한 개, 두 개 또는 세 개의 매개 변수를 사용하는 방법은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|DocId|**bigint**|키 값에 해당하는 내부 문서 ID(DocId) 열입니다.|  
|Key|*|지정한 테이블의 전체 텍스트 키 값입니다.<br /><br /> 매핑 테이블에 전체 텍스트 키가 없으면 빈 행 집합이 반환됩니다.|  
  
 <sup>*</sup> 키에 대 한 데이터 형식이 기본 테이블의 전체 텍스트 키 열의 데이터 형식으로 동일 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 함수는 공개 함수이며 특별한 사용 권한이 필요하지 않습니다.  
  
## <a name="remarks"></a>설명  
 다음 표에서는 한 개, 두 개 또는 세 개의 매개 변수를 사용한 결과에 대해 설명합니다.  
  
|이 매개 변수 목록|이 결과가 하는 중...|  
|--------------------------|----------------------|  
|*table_id*|만 사용 하 여 호출 하는 경우는 *table_id* 매개 변수를 sp_fulltext_keymappings는 함께 각 키에 해당 하는 DocId 지정된 된 기본 테이블에서 모든 전체 텍스트 키 (키) 값을 반환 합니다. 여기에는 삭제가 보류된 키가 포함됩니다.<br /><br /> 이 함수는 다양한 문제를 해결하는 데 유용합니다. 특히, 선택한 전체 텍스트 키가 정수 데이터 형식이 아닐 경우 전체 텍스트 인덱스 내용을 보는 데 유용합니다. 이 경우 sp_fulltext_keymappings의 결과 사용 하 여 결과 조인 해야 **sys.dm_fts_index_keywords_by_document**합니다. 자세한 내용은 [sys.dm_fts_index_keywords_by_document &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)합니다.<br /><br /> 그러나 일반적으로는 가능하면 sp_fulltext_keymappings를 특정 전체 텍스트 키나 DocId를 지정하는 매개 변수와 함께 실행하는 것이 좋습니다. 이 방법은 전체 키 맵을 반환하는 것보다 훨씬 효율적입니다. 특히 매우 큰 테이블의 경우 전체 키 맵을 반환하기 위한 성능 비용이 상당히 크므로 더욱 효율적입니다.|  
|*table_id*, *docid*|경우에 합니다 *table_id* 및 *docid* 지정 된 *docid* null이 아니어야 하 고 지정된 된 테이블의 올바른 DocId를 지정 해야 합니다. 이 함수는 특정 전체 텍스트 인덱스의 DocId에 해당하는 기본 테이블에서 사용자 지정 전체 텍스트 키를 분리하는 데 유용합니다.|  
|*table_id*, NULL, *key*|두 번째 매개 변수는 NULL 이어야 세 개의 매개 변수가 있는 경우 및 *키* null이 아니어야 하 고 지정된 된 테이블의 유효한 전체 텍스트 키 값을 지정 해야 합니다. 이 함수는 특정 전체 텍스트 키에 해당하는 DocId를 기본 테이블에서 분리하는 데 유용합니다.|  
  
 다음과 같은 경우 오류가 반환됩니다.  
  
-   잘못 된 지정할 *table_id*합니다.  
  
-   테이블이 전체 텍스트 인덱싱되지 않은 경우  
  
-   NULL이 아닐 수 있는 매개 변수에 대해 NULL이 발생한 경우  
  
## <a name="examples"></a>예  
  
> [!NOTE]  
>  이 섹션의 예에서는 `Production.ProductReview` 예제 데이터베이스의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 테이블을 사용합니다. 제공 하는 예제를 실행 하 여이 인덱스를 만들 수 있습니다 합니다 `ProductReview` 테이블의 [CREATE FULLTEXT INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)합니다.  
  
### <a name="a-obtaining-all-the-key-and-docid-values"></a>A. 모든 Key 및 DocId 값 가져오기  
 다음 예제에서는 [DECLARE](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 지역 변수를 만들고 문을 `@table_id` 의 ID를 할당할 수는 `ProductReview` 테이블로 해당 값입니다. 이 예제를 실행 **sp_fulltext_keymappings** 지정 `@table_id` 에 대 한 합니다 *table_id* 매개 변수입니다.  
  
> [!NOTE]  
>  사용 하 여 **sp_fulltext_keymappings** 만 합니다 *table_id* 매개 변수는 작은 테이블에 적합 합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id;  
GO  
  
```  
  
 이 예에서는 다음과 같이 테이블에서 모든 DocId 및 전체 텍스트 키를 반환합니다.  
  
||||  
|-|-|-|  
||`docid`|`key`|  
|`1`|`1`|`1`|  
|`2`|`2`|`2`|  
|`3`|`3`|`3`|  
|`4`|`4`|`4`|  
  
### <a name="b-obtaining-the-docid-value-for-a-specific-key-value"></a>2\. 특정 Key 값에 대한 DocId 값 가져오기  
 다음 예에서는 DECLARE 문을 사용하여 지역 변수 `@table_id`를 만들고 `ProductReview` 테이블의 ID를 해당 값으로 할당합니다. 예제를 실행 **sp_fulltext_keymappings** 지정 `@table_id` 에 대 한 합니다 *table_id* 매개 변수를 NULL에 대 한 합니다 *docid* 매개 변수 및 4는 *키* 매개 변수입니다.  
  
> [!NOTE]  
>  사용 하 여 **sp_fulltext_keymappings** 만 합니다 *table_id* 변수가 작은 테이블에 적합 합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id, NULL, 4;  
GO  
  
```  
  
 이 예에서는 다음 결과를 반환합니다.  
  
||||  
|-|-|-|  
||`docid`|`key`|  
|`4`|`4`|`4`|  
  
## <a name="see-also"></a>관련 항목  
 [전체 텍스트 검색과 의미 체계 검색 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
