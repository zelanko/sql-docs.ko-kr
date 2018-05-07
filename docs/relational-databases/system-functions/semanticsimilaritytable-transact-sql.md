---
title: semanticsimilaritytable (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- semanticsimilaritytable
- semanticsimilaritytable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritytable function
ms.assetid: b49d40ab-7552-438b-ad67-6237dcccb75b
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8b6b4b36580c35aead16780f4ada0f461dd58754
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="semanticsimilaritytable-transact-sql"></a>semanticsimilaritytable(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  지정된 열의 내용이 지정된 문서와 의미상 유사한 0개 이상의 문서 행으로 구성된 테이블을 반환합니다.  
  
 SELECT 문의 FROM 절에서 이 행 집합 함수를 일반 테이블 이름처럼 참조할 수 있습니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
SEMANTICSIMILARITYTABLE  
    (  
    table,  
    { column | (column_list) | * },  
    source_key  
    )  
```  
  
##  <a name="Arguments"></a> 인수  
 **table**  
 전체 텍스트 및 의미 체계 인덱싱을 사용하도록 설정된 테이블의 이름입니다.  
  
 이 이름은 1~4개의 부분으로 구성된 이름일 수 있지만 원격 서버 이름은 사용할 수 없습니다.  
  
 **column**  
 결과가 반환될 인덱싱된 열의 이름입니다. 열에 의미 체계 인덱싱이 사용하도록 설정되어 있어야 합니다.  
  
 **column_list**  
 쉼표로 구분되고 괄호로 묶인 여러 열을 나타냅니다. 모든 열에 의미 체계 인덱싱이 사용하도록 설정되어 있어야 합니다.  
  
 **\***  
 의미 체계 인덱싱이 사용하도록 설정된 모든 열이 포함되어 있음을 나타냅니다.  
  
 **source_key**  
 특정 행에 대한 결과를 요청할 행의 고유 키입니다.  
  
 이 키는 가능한 경우 원본 테이블의 전체 텍스트 고유 키와 같은 형식으로 암시적으로 변환됩니다. 상수나 변수로 키를 지정할 수 있지만 식 또는 스칼라 하위 쿼리의 결과를 키로 지정할 수는 없습니다.  
  
## <a name="table-returned"></a>반환된 테이블  
 다음 표에서는 이 행 집합 함수가 반환하는 유사하거나 관련된 문서에 대해 설명합니다.  
  
 결과가 둘 이상의 열에서 요청된 경우에는 열 단위로 대응 문서가 반환됩니다.  
  
|Column_name|형식|Description|  
|------------------|----------|-----------------|  
|**source_column_id**|**int**|유사한 문서를 찾는 데 사용된 원본 문서의 열 ID입니다.<br /><br /> column_id에서 열 이름을 검색하거나 열 이름에서 column_id를 검색하는 방법에 대한 자세한 내용은 COL_NAME 및 COLUMNPROPERTY 함수를 참조하십시오.|  
|**matched_column_id**|**int**|유사한 문서를 찾은 열의 ID입니다.<br /><br /> column_id에서 열 이름을 검색하거나 열 이름에서 column_id를 검색하는 방법에 대한 자세한 내용은 COL_NAME 및 COLUMNPROPERTY 함수를 참조하십시오.|  
|**matched_document_key**|**\***<br /><br /> 이 키는 원본 테이블의 고유 키 유형과 일치합니다.|쿼리에서 지정된 문서와 유사한 것으로 확인된 문서나 행의 전체 텍스트 및 의미 체계 추출 고유 키 값입니다.|  
|**score**|**REAL**|유사한 다른 모든 문서를 기준으로 한 이 문서의 상대적 유사성 값입니다.<br /><br /> 이 값은 [0.0, 1.0] 범위의 소수 10진수 값입니다. 점수가 높을수록 유사성이 높으며 1.0이 최대 점수입니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 참조 [유사한 찾기 및 의미 체계 검색을 사용 하 여 관련 문서](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 유사한 문서의 열 간에는 쿼리할 수 없습니다. **SEMANTICSIMILARITYTABLE** 함수에 의해 식별 되는 원본 열과 동일한 열에서 유사 문서 검색는 **source_key** 인수입니다.  
  
## <a name="metadata"></a>메타데이터  
 의미 체계 유사성 추출 및 채우기에 대한 정보와 상태를 보려면 다음 동적 관리 뷰를 쿼리합니다.  
  
-   [sys.dm_db_fts_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 전체 텍스트 및 의미 체계 인덱스를 만든 기본 테이블에 대한 SELECT 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 AdventureWorks2012 예제 데이터베이스의 HumanResources.JobCandidate 테이블에서 지정된 입사 지원자와 유사한 최상위 10명의 입사 지원자를 검색합니다.  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROMSEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
