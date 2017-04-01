---
title: "RANK를 사용하여 검색 결과 제한 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "행 순위 [전체 텍스트 검색]"
  - "관련성 순위 값 [전체 텍스트 검색]"
  - "전체 텍스트 검색 [SQL Server], 순위"
  - "인덱스 순위 [전체 텍스트 검색]"
  - "순위 결과 [전체 텍스트 검색]"
  - "순위 [전체 텍스트 검색]"
  - "행 기준 순위 값 [전체 텍스트 검색]"
ms.assetid: 06a776e6-296c-4ec7-9fa5-0794709ccb17
caps.latest.revision: 20
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 19
---
# RANK를 사용하여 검색 결과 제한
  [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 및 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 함수는 0부터 1000까지의 서수 값(순위 값)이 포함된 RANK라는 열을 반환합니다. 이러한 값은 반환된 행이 선택 조건에 얼마나 일치하는지에 따라 순위를 매기는 데 사용됩니다. 순위 값은 결과 집합에 포함된 행의 관련성을 나타내는 상대적 순서일 뿐이며 값이 작을수록 관련이 없는 것입니다. 실제 값은 중요하지 않으며 일반적으로 쿼리가 실행될 때마다 달라집니다.  
  
> [!NOTE]  
>  CONTAINS 및 FREETEXT 조건자는 순위 값을 반환하지 않습니다.  
  
 검색 조건과 일치하는 항목 수는 종종 매우 많습니다. CONTAINSTABLE 또는 FREETEXTTABLE 쿼리가 반환하는 일치하는 항목 수를 줄이려면 행의 하위 집합만 반환하는 선택적 *top_n_by_rank* 매개 변수를 사용합니다. *top_n_by_rank*는 내림차순으로 최고 등급 *n*개의 일치하는 항목만 반환되도록 지정하는 정수 값 *n*입니다. *top_n_by_rank*를 다른 매개 변수와 함께 사용하면 실제로 모든 조건자와 일치하는 행 수보다 적은 수의 행이 반환될 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 일치하는 항목을 순위별로 정렬하고 지정한 개수만 반환합니다. 이 방법을 사용하면 성능이 크게 향상됩니다. 예를 들어 백만 개의 행이 있는 테이블에서 100,000개의 행을 반환하는 쿼리에 대해 상위 100개의 행만 요청하면 쿼리가 훨씬 빨리 처리됩니다.  
  
##  <a name="examples"></a> 순위를 사용하여 검색 결과를 제한하는 예  
  
### 예 A: 상위 3개의 일치하는 항목만 검색  
 다음 예제에서는 CONTAINSTABLE을 사용하여 상위 3개의 일치하는 항목만 반환합니다.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT K.RANK, AddressLine1, City  
FROM Person.Address AS A  
  INNER JOIN  
  CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("des*",  
    Rue WEIGHT(0.5),  
    Bouchers WEIGHT(0.9))',  
    3) AS K  
  ON A.AddressID = K.[KEY]  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
RANK        Address                          City  
----------- -------------------------------- ------------------------------  
172         9005, rue des Bouchers           Paris  
172         5, rue des Bouchers              Orleans  
172         5, rue des Bouchers              Metz  
  
(3 row(s) affected)  
```  
  
 [항목 내용](#top)  
  
### 예 B: 상위 10개의 일치하는 항목 검색  
 다음 예에서는 CONTAINSTABLE을 사용하여 `Description` 열에 "light"나 "lightweight"라는 단어와 근접한 "aluminum"이라는 단어가 포함된 상위 5개 제품에 대한 설명을 반환합니다.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
GO  
```  
  
 [항목 내용](#top)  
  
##  <a name="how"></a> 검색 쿼리 결과의 순위를 지정하는 방법  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 전체 텍스트 검색은 전체 텍스트 쿼리가 반환하는 데이터의 관련성을 나타내는 선택적 점수(또는 순위 값)를 생성할 수 있습니다. 이 순위 값은 모든 행에 대해 계산되고 지정된 쿼리의 결과 집합을 관련 순으로 정렬하는 정렬 조건으로 사용될 수 있습니다. 순위 값은 결과 집합에 포함된 행의 관련성을 나타내는 상대적 순서일 뿐입니다. 실제 값은 중요하지 않으며 일반적으로 쿼리가 실행될 때마다 달라집니다. 순위 값은 전체 쿼리에서 아무 의미도 갖지 않습니다.  
  
### 순위용 통계  
 인덱스를 작성할 때 순위에 사용할 통계가 수집됩니다. 전체 텍스트 카탈로그의 작성 과정에서 직접 단일 인덱스 구조가 생성되는 것은 아닙니다. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 전체 텍스트 검색 엔진은 데이터가 인덱싱될 때 중간 인덱스를 만듭니다. 그런 다음 전체 텍스트 검색 엔진은 필요에 따라 이러한 인덱스를 큰 인덱스로 병합합니다. 이 프로세스는 여러 번 반복할 수 있습니다. 최종적으로 전체 텍스트 검색 엔진은 모든 중간 인덱스를 큰 마스터 인덱스로 결합하는 "마스터 병합"을 수행합니다.  
  
 통계는 각 중간 인덱스 수준에서 수집됩니다. 인덱스를 병합할 때 통계도 병합됩니다. 일부 통계 값은 마스터 병합 프로세스 중에만 생성할 수 있습니다.  
  
 쿼리 결과 집합의 순위를 지정할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 가장 큰 중간 인덱스의 통계를 사용합니다. 이는 중간 인덱스의 병합 여부에 따라 결정됩니다. 따라서 중간 인덱스가 병합되지 않은 경우 순위 통계의 정확도가 달라질 수 있습니다. 이런 이유로 시간이 경과하면서 전체 텍스트 인덱싱된 데이터가 추가, 수정 및 삭제되고 작은 인덱스가 병합됨에 따라 동일한 쿼리에서 여러 순위 결과가 반환될 수 있습니다.  
  
 인덱스 크기와 복잡한 계산을 최소화하기 위해 통계를 반올림하는 경우가 많습니다.  
  
 아래 목록에는 자주 사용하는 용어와 순위 계산 시 중요한 통계 값이 포함되어 있습니다.  
  
 속성  
 행의 전체 텍스트 인덱싱된 열입니다.  
  
 문서  
 쿼리에서 반환된 엔터티입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 문서는 행에 해당합니다. 행이 여러 개의 전체 텍스트 인덱싱된 열을 가질 수 있는 것처럼 문서는 여러 속성을 가질 수 있습니다.  
  
 인덱스  
 하나 이상의 문서에 대해 반전된 단일 인덱스입니다. 인덱스 전체가 메모리나 디스크에 포함될 수 있습니다. 많은 쿼리 통계는 항목이 일치한 개별 인덱스를 기준으로 합니다.  
  
 전체 텍스트 카탈로그  
 쿼리에 대해 하나의 엔터티로 처리되는 중간 인덱스 컬렉션입니다. 카탈로그는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자에게 표시되는 조직 구성 단위입니다.  
  
 단어, 토큰 또는 항목  
 전체 텍스트 검색 엔진에서 일치하는 단위입니다. 문서의 텍스트 스트림은 언어별 단어 분리기에 의해 단어 또는 토큰으로 토큰화됩니다.  
  
 발생 빈도  
 단어 분리기에서 결정된 문서 속성의 단어 오프셋입니다. 첫 번째 단어는 발생 빈도 1, 다음 단어는 발생 빈도 2 등으로 지정됩니다. 구 및 근접 쿼리에서 잘못된 단어가 검색되는 것을 방지하기 위해 문장 끝(End-of-Sentence)과 단락 끝(End-of-Paragraph)으로 발생 간격을 늘립니다.  
  
 TermFrequency  
 해당 키 값이 행에서 나오는 횟수입니다.  
  
 IndexedRowCount  
 인덱싱된 전체 행 수입니다. 이 개수는 중간 인덱스에서 유지 관리되는 행 수를 기준으로 계산되므로 정확도가 달라질 수 있습니다.  
  
 KeyRowCount  
 전체 텍스트 카탈로그에서 지정된 키가 포함된 전체 행 수입니다.  
  
 MaxOccurrence  
 지정된 행 속성에 대해 전체 텍스트 카탈로그에 저장된 최대 발생 횟수입니다.  
  
 MaxQueryRank  
 전체 텍스트 검색 엔진에서 반환된 최대 순위로 1000입니다.  
  
 [항목 내용](#top)  
  
### 순위 계산 문제  
 많은 요소가 순위 계산 과정에 영향을 줍니다.  각 언어별 단어 분리기는 텍스트를 다르게 토큰화합니다. 예를 들어 "dog-house"란 문자열을 특정 단어 분리기는 "dog" "house"로 분리하고 다른 단어 분리기는 "dog-house"로 분리할 수 있습니다. 즉, 단어뿐만 아니라 문서 길이도 다르기 때문에 지정된 언어에 따라 일치 항목과 순위가 달라집니다. 문서 길이의 차이는 모든 쿼리의 순위에 영향을 줄 수 있습니다.  
  
 **IndexRowCount** 와 같은 통계는 크게 달라질 수 있습니다. 예를 들어 카탈로그의 마스터 인덱스에 20억 개 행이 있고 메모리 내 중간 인덱스에 하나의 새 문서가 인덱싱되면 메모리 내 인덱스의 문서 수를 기준으로 한 해당 문서의 순위와 마스터 인덱스 문서에 대한 순위에 차이가 생길 수 있습니다. 이런 이유로 다수의 행이 인덱싱 또는 다시 인덱싱 채우기 후에는 ALTER FULLTEXT CATALOG ... REORGANIZE [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 인덱스를 마스터 인덱스에 병합하는 것이 좋습니다. 또한 전체 텍스트 검색 엔진은 중간 인덱스의 개수와 크기 같은 매개 변수를 기준으로 인덱스를 자동으로 병합합니다.  
  
 **MaxOccurrence** 값은 32개 범위 중 하나로 정규화됩니다. 예를 들어 이것은 50단어 길이의 문서가 100단어 길이의 문서와 동일하게 처리된다는 것을 의미합니다. 정규화에 사용되는 표는 아래와 같습니다. 문서 길이가 둘 다 인접 테이블 값 32와 128 사이의 범위에 있기 때문에 실제로 두 문서는 모두 길이가 128인 것으로 처리됩니다(32 < **docLength** <= 128).  
  
```  
{ 16, 32, 128, 256, 512, 725, 1024, 1450, 2048, 2896, 4096, 5792, 8192, 11585,   
16384, 23170, 28000, 32768, 39554, 46340, 55938, 65536, 92681, 131072, 185363,   
262144, 370727, 524288, 741455, 1048576, 2097152, 4194304 };  
  
```  
  
 [항목 내용](#top)  
  
### CONTAINSTABLE 순위  
 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 순위는 다음 알고리즘을 사용합니다.  
  
```  
StatisticalWeight = Log2( ( 2 + IndexedRowCount ) / KeyRowCount )  
Rank = min( MaxQueryRank, HitCount * 16 * StatisticalWeight / MaxOccurrence )  
```  
  
 구 일치는 **KeyRowCount**(구가 포함된 행 수)가 예상 개수이므로 부정확하고 실제 개수보다 많을 수 있는 점을 제외하고 개별 키와 마찬가지로 순위가 지정됩니다.  
  
 **NEAR 순위**  
  
 CONTAINSTABLE은 NEAR 옵션을 사용하여 서로 근접한 검색 단어를 두 개 이상 쿼리하는 기능을 지원합니다. 반환된 각 행의 순위 값은 여러 매개 변수를 기반으로 합니다. 하나의 주 순위 요인은 문서 길이에 대한 총 일치 항목(*적중*) 수입니다. 따라서 100단어 문서와 900단어 문서에 동일한 일치 항목이 있는 경우 100단어 문서의 순위가 보다 높게 지정됩니다.  
  
 행에서의 각 적중에 대한 총 길이도 해당 적중의 첫 번째 검색 용어와 마지막 검색 요소 간의 거리를 기준으로 하는 해당 행의 순위에 영향을 줍니다. 이 거리가 더 가까울수록 적중이 행 순위 값에 끼치는 영향이 더 커집니다. 전체 텍스트 쿼리가 정수를 최대 거리로 지정하지 않는 경우 거리가 100개 논리적 용어 이상 떨어져 있는 적중만 포함하는 문서의 순위는 0이 됩니다.  
  
 **ISABOUT 순위**  
  
 CONTAINSTABLE은 ISABOUT 옵션을 사용하여 가중치 용어를 쿼리하는 것을 지원합니다. ISABOUT은 일반적인 정보 검색 용어로 벡터 공간 쿼리를 의미합니다. 사용되는 기본 순위 알고리즘은 널리 알려진 수식인 Jaccard입니다. 순위는 쿼리의 각 단어에 대해 계산된 다음 아래에 설명된 것처럼 결합됩니다.  
  
```  
ContainsRank = same formula used for CONTAINSTABLE ranking of a single term (above).  
Weight = the weight specified in the query for each term. Default weight is 1.  
WeightedSum = Σ[key=1 to n] ContainsRankKey * WeightKey  
Rank =  ( MaxQueryRank * WeightedSum ) / ( ( Σ[key=1 to n] ContainsRankKey^2 )   
      + ( Σ[key=1 to n] WeightKey^2 ) - ( WeightedSum ) )  
  
```  
  
 [항목 내용](#top)  
  
### FREETEXTTABLE 순위  
 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 순위는 OKAPI BM25 순위 수식을 기준으로 합니다. FREETEXTTABLE 쿼리는 활용 생성(원래 쿼리 단어의 활용 형태)을 통해 쿼리에 단어를 추가합니다. 이러한 단어는 원래 단어와 특별한 관계없이 별도의 단어로 처리됩니다. 사전 기능에서 생성된 동의어도 가중치가 같은 별도의 단어로 처리됩니다. 쿼리의 각 단어가 순위에 영향을 줍니다.  
  
```  
Rank = Σ[Terms in Query] w ( ( ( k1 + 1 ) tf ) / ( K + tf ) ) * ( ( k3 + 1 ) qtf / ( k3 + qtf ) ) )  
Where:   
w is the Robertson-Sparck Jones weight.   
In simplified form, w is defined as:   
w = log10 ( ( ( r + 0.5 ) * ( N – R + r + 0.5 ) ) / ( ( R – r + 0.5 ) * ( n – r + 0.5 ) )  
N is the number of indexed rows for the property being queried.   
n is the number of rows containing the word.   
K is ( k1 * ( ( 1 – b ) + ( b * dl / avdl ) ) ).   
dl is the property length, in word occurrences.   
avdl is the average length of the property being queried, in word occurrences.   
k1, b, and k3 are the constants 1.2, 0.75, and 8.0, respectively.   
tf is the frequency of the word in the queried property in a specific row.   
qtf is the frequency of the term in the query.   
```  
  
 [항목 내용](#top)  
  
## 참고 항목  
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)  
  
  