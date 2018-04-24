---
title: NEAR를 사용하여 근접 단어 검색 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- word searches [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- proximity searches [full-text search]
- full-text search [SQL Server], proximity searches
- full-text queries [SQL Server], proximity
- queries [full-text search], proximity
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
caps.latest.revision: 65
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 00e3df715e7a608c47eff977448d20f6364a467c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="search-for-words-close-to-another-word-with-near"></a>NEAR를 사용하여 근접 단어 검색
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 조건자 또는 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 함수에서 *근접 단어* **NEAR**를 사용하여 단어나 구를 검색할 수 있습니다. 
  
##  <a name="Custom_NEAR"></a> NEAR 개요  
**NEAR**에는 다음과 같은 기능이 포함되어 있습니다.  
-   첫 번째 검색 단어와 마지막 검색 단어를 분리하는 검색 대상이 아닌 단어의 최대 수를 지정할 수 있습니다.

-   임의의 순서 또는 특정 순서로 단어 또는 구를 검색할 수 있습니다.
  
-   일치 항목이 되기 위한 첫 번째 검색 단어와 마지막 검색 단어를 분리하는 검색 대상이 아닌 단어의 최대 수( *최대 거리*)를 지정할 수 있습니다.  

-   최대 단어 수를 지정하는 경우 일치 항목이 지정된 순서로 검색 단어를 포함하도록 지정할 수도 있습니다.

 
 일치 항목이 되려면 텍스트 문자열은 다음 조건을 충족해야 합니다.  
  
-   지정된 검색 단어 중 하나로 시작하고 지정된 다른 검색 단어 중 하나로 끝납니다.  
  
-   지정된 검색 단어를 모두 포함합니다.  
  
-   중지 단어를 포함하여 첫 번째 검색 단어와 마지막 검색 단어 사이에 있는 검색 대상이 아닌 단어의 수는 최대 거리가 지정된 경우 최대 거리보다 작거나 같아야 합니다.  
  
## <a name="syntax-of-near"></a>NEAR 구문
**NEAR**의 기본 구문은 다음과 같습니다.  

``` 
 NEAR (  
  
 {  
  
 *search_term* [ ,…*n* ]  
  
 |  
  
 (*search_term* [ ,…*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
```

구문에 대한 자세한 내용은 [CONTAINS&#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)를 참조하세요.  

## <a name="examples"></a>예
### <a name="example-1"></a>예 1
 예를 들어 다음과 같이 'Smith'와의 사이에 최대 두 단어가 있는 'John'을 검색할 수 있습니다.  
  
```sql
... CONTAINS(column_name, 'NEAR((John, Smith), 2)')
```  
  
 일치하는 문자열의 예로는 "`John Jacob Smith`" 및 "`Smith, John`" 등이 있습니다. 문자열 "`John Jones knows Fred Smith`"는 두 단어 사이에 검색 대상이 아닌 단어가 3개 있으므로 일치 항목이 아닙니다.  
  
 특정 순서로 단어를 찾으려면 예에 있는 근접 단어를 `NEAR((John, Smith),2, TRUE).` 로 변경합니다. 이제 "`John`"와 두 단어 거리 이내에서 "`Smith`"을 검색하지만 "`John`"이 "`Smith`"의 앞에 있어야 합니다. 영어와 같이 왼쪽에서 오른쪽으로 읽는 언어에서 일치하는 문자열의 예로는 "`John Jacob Smith`"가 있습니다.  
  
 아랍어나 히브리어와 같이 오른쪽에서 왼쪽으로 읽는 언어에서는 전체 텍스트 엔진이 지정된 단어를 반대 방향으로 적용합니다. 또한 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 개체 탐색기는 오른쪽에서 왼쪽으로 읽는 언어로 지정된 단어의 표시 순서를 자동으로 전환합니다.   

### <a name="example-2"></a>예제 2
 다음 예에서는 `Production.Document` 샘플 데이터베이스의 `AdventureWorks` 테이블에서 "bracket"이라는 단어와 동일한 문서에 "reflector"라는 단어가 들어 있는 모든 문서 요약을 검색합니다.  
  
```sql
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
``` 
 
## <a name="how-maximum-distance-is-measured"></a>최대 거리를 측정하는 방법  
 10 또는 25와 같은 특정 최대 거리는 지정된 문자열에서 중지 단어를 포함하여 첫 번째 검색 단어와 마지막 검색 단어 사이에 있는 검색 대상이 아닌 단어의 수를 결정합니다. 예를 들어 `NEAR((dogs, cats, "hunting mice"), 3)` 는 검색 대상이 아닌 단어 수가 총 3개("`enjoy`", "`but`" 및 "`avoid`")인 다음 행을 반환합니다.  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 이 근접 단어는 검색 대상이 아닌 단어가 4개("`enjoy`", "`but`", "`usually`" 및 "`avoid`")여서 최대 거리가 초과된 다음 행을 반환하지 않습니다.  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
## <a name="combine-near-with-other-terms"></a>NEAR와 다른 용어 결합  
 NEAR를 일부 다른 용어와 결합할 수 있습니다. AND(&), OR(|) 또는 AND NOT(&!)을 사용하여 사용자 지정 근접 단어를 다른 사용자 지정 근접 단어, 단순 단어 또는 접두사 단어와 결합할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NEAR((*term3*, *term4*),2)')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR NEAR((*term3*, *term4*),2, TRUE)')  
  
 예:  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 NEAR와 생성 용어(ISABOUT ...) 또는 가중치 용어(FORMSOF ...)를 결합할 수 없습니다.  
  
##  <a name="Additional_Considerations"></a> 근접 검색에 대한 추가 정보  
   
-   검색 단어가 겹쳐서 나타남  
  
     모든 근접 검색은 검색 단어가 겹치지 않는 경우만 검색합니다. 검색 단어가 겹쳐서 나타나는 경우 일치 항목이 될 수 없습니다. 예를 들어 다음 근접 단어는 최대 거리를 두 단어로 지정하여 "`A`" 및 "`AA`"를 이 순서대로 검색합니다.  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     가능한 일치 항목은 "`AAA`", "`A.AA`" 및 "`A..AA`" 등입니다. "`AA`"만 포함하는 행은 일치 항목이 아닙니다.  
  
    > [!NOTE]  
    >  예를 들어 `NEAR("mountain bike", "bike trails")` 또는 `(NEAR(comfort*, comfortable), 5)`와 같이 겹치는 단어를 지정할 수 있습니다. 겹치는 단어를 지정하면 일치하는 항목의 가능한 조합이 늘어나므로 쿼리의 복잡도가 높아집니다. 이렇게 겹치는 단어를 많이 지정하면 쿼리가 리소스 부족으로 실패할 수 있습니다. 이런 경우 쿼리를 단순화한 다음 다시 시도하십시오.  
  
-   NEAR는 최대 거리 지정 여부에 관계없이 용어 간 절대 거리가 아닌 논리적 거리를 나타냅니다. 예를 들어 단락 내에서 다른 구 또는 문장에 있는 단어는 관련이 더 적다고 가정하므로 실제 근접성에 관계없이 같은 구 또는 문장에 있는 단어보다 더 멀리 떨어져 있는 것으로 간주됩니다. 마찬가지로 다른 단락에 있는 단어는 이보다도 더 많이 떨어져 있는 것으로 간주됩니다. 일치 항목이 문장, 단락 또는 장의 끝을 넘어가면 문서의 순위를 지정하는 데 사용되는 간격이 각각 8, 128 또는 1024만큼 늘어납니다.  
  
-   CONTAINSTABLE 함수의 순위 지정에 근접 단어가 미치는 영향  
  
    CONTAINSTABLE 함수에서 NEAR를 사용하는 경우 문서 길이에 상대적인 문서 내 적중 수와 각 적중의 첫 번째 검색 단어와 마지막 검색 단어 간 거리가 각 문서의 순위에 영향을 줍니다. 일반 근접 단어의 경우 일치하는 검색 단어가 논리적 단어 50개보다 더 떨어져 있으면 문서에 대해 반환되는 순위는 0입니다. 최대 거리로 정수를 지정하지 않은 사용자 지정 근접 단어의 경우 간격이 논리적 단어 100개보다 더 떨어져 있는 적중만 포함된 문서의 순위는 0이 됩니다. 사용자 지정 근접 검색의 순위 지정에 대한 자세한 내용은 [Limit Search Results with RANK](../../relational-databases/search/limit-search-results-with-rank.md)을 참조하십시오.  
  
-   **의미 없는 단어 변환** 서버 옵션  
  
     근접 검색에 중지 단어가 지정된 경우 **의미 없는 단어 변환** 의 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 중지 단어를 처리하는 방법에 영향을 미칩니다. 자세한 내용은 [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)을 참조하세요.   
  
## <a name="see-also"></a>참고 항목  
 [CONTAINS&#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
