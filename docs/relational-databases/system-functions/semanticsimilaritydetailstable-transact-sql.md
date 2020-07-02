---
title: semanticsimilaritydetailstable (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semanticsimilaritydetailstable
- semanticsimilaritydetailstable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritydetailstable function
ms.assetid: 038d751a-fca5-4b4c-9129-cba741a4e173
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4b264f5276ad9d9f411fcdd14550130eb412a1b0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771559"
---
# <a name="semanticsimilaritydetailstable-transact-sql"></a>semanticsimilaritydetailstable(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  의미상 유사한 내용의 두 문서(원본 문서 및 대응 문서) 간에 공통적인 키 구가 있는 0개 이상의 행으로 구성된 테이블을 반환합니다.  
  
 SELECT 문의 FROM 절에서이 행 집합 함수를 참조할 수 있습니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
SEMANTICSIMILARITYDETAILSTABLE  
    (  
    table,  
    source_column,  
    source_key,  
    matched_column,  
    matched_key  
    )  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>인수의  
 **table**  
 전체 텍스트 및 의미 체계 인덱싱을 사용하도록 설정된 테이블의 이름입니다.  
  
 이 이름은 1~4개의 부분으로 구성된 이름일 수 있지만 원격 서버 이름은 사용할 수 없습니다.  
  
 **source_column**  
 비슷한지 비교할 내용이 포함된 원본 행의 열 이름입니다.  
  
 **source_key**  
 원본 문서의 행을 나타내는 고유한 키입니다.  
  
 이 키는 가능한 경우 원본 테이블의 전체 텍스트 고유 키와 같은 유형으로 암시적으로 변환됩니다. 상수나 변수로 키를 지정할 수 있지만 식 또는 스칼라 하위 쿼리의 결과를 키로 지정할 수는 없습니다. 잘못된 키를 지정하면 행이 반환되지 않습니다.  
  
 **matched_column**  
 비슷한지 비교할 내용이 포함된 대응하는 행의 열 이름입니다.  
  
 **matched_key**  
 대응 문서의 행을 나타내는 고유한 키입니다.  
  
 이 키는 가능한 경우 원본 테이블의 전체 텍스트 고유 키와 같은 유형으로 암시적으로 변환됩니다. 상수나 변수로 키를 지정할 수 있지만 식 또는 스칼라 하위 쿼리의 결과를 키로 지정할 수는 없습니다.  
  
## <a name="table-returned"></a>반환된 테이블  
 다음 표에서는 이 행 집합 함수가 반환하는 키 구에 대해 설명합니다.  
  
|Column_name|형식|설명|  
|------------------|----------|-----------------|  
|**키 구**|**VARCHAR**|원본 문서와 대응 문서 간의 유사성에 기여하는 키 구.|  
|**점수**|**실제로**|두 문서 간에 유사성이 있는 다른 모든 키 구를 기준으로 한 이 키 구의 상대적 값입니다.<br /><br /> 이 값은 [0.0, 1.0] 범위의 소수 10진수 값입니다. 점수가 높을수록 유사성이 높으며 1.0이 최대 점수입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 [의미 체계 검색을 사용 하는 유사 및 관련 문서 찾기](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)를 참조 하세요.  
  
## <a name="metadata"></a>메타데이터  
 의미 체계 유사성 추출 및 채우기에 대한 정보와 상태를 보려면 다음 동적 관리 뷰를 쿼리합니다.  
  
-   [sys.dm_db_fts_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 전체 텍스트 및 의미 체계 인덱스를 만든 기본 테이블에 대한 SELECT 권한이 있어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 AdventureWorks2012 예제 데이터베이스의 **HumanResources 후보** 테이블에서 지정 된 후보 사이에 가장 높은 유사성 점수가 있는 5 개의 키 구를 검색 합니다. @CandidateId및 @MatchedID 변수는 전체 텍스트 인덱스의 키 열에 있는 값을 나타냅니다.  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROMSEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
