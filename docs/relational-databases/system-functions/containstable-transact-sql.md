---
description: CONTAINSTABLE(Transact-SQL)
title: CONTAINSTABLE (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CONTAINSTABLE
- CONTAINSTABLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- precise or fuzzy (less precise) matches [full-text search]
- fuzzy (less precise) word or phrase search [full-text search]
- word searches [full-text search]
- weighted values [full-text search]
- values [SQL Server], ranked
- LANGUAGE option
- NEAR option [full-text search]
- RANK column
- phrase searches [full-text search]
- conditions [SQL Server], CONTAINSTABLE
- relevance ranking values [full-text search]
- proximity searches [full-text search]
- CONTAINSTABLE function (Transact-SQL)
- ranked results [full-text search]
- rankings [full-text search]
- less precise (fuzzy) searches [full-text search]
ms.assetid: e580c210-cf57-419d-9544-7f650f2ab814
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ae9077610031075f71564eb5938b2a1415842827
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454800"
---
# <a name="containstable-transact-sql"></a>CONTAINSTABLE(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  특정 단어나 구와 정확히 일치하거나 비슷하게 일치하는 단어 검색, 서로 근접한 단어 검색 또는 가중치 검색에서 일치하는 항목이 포함된 열에 대해 0개 이상의 행이 있는 테이블을 반환합니다. CONTAINSTABLE은 SELECT 문의 [FROM 절](../../t-sql/queries/from-transact-sql.md) 에 사용 [!INCLUDE[tsql](../../includes/tsql-md.md)] 되며 일반 테이블 이름인 것 처럼 참조 됩니다. 문자 기반 데이터 형식을 포함하는 전체 텍스트 인덱싱된 열에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색을 수행합니다.  
  
 CONTAINSTABLE은 [contains 조건자](../../t-sql/queries/contains-transact-sql.md) 와 동일한 종류의 일치에 유용 하며 contains와 동일한 검색 조건을 사용 합니다.  
  
 그러나 CONTAINS와 달리, CONTAINSTABLE을 사용한 쿼리는 각 행에 대해 적절한 등급 값(RANK) 및 전체 텍스트 키(KEY)를 반환합니다.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 전체 텍스트 검색 형식에 대한 자세한 내용은 [전체 텍스트 검색이 있는 쿼리](../../relational-databases/search/query-with-full-text-search.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CONTAINSTABLE   
( table , { column_name | ( column_list ) | * } , ' <contains_search_condition> '   
     [ , LANGUAGE language_term]   
  [ , top_n_by_rank ]   
)   
  
<contains_search_condition> ::=   
    { <simple_term>   
    | <prefix_term>   
    | <generation_term>   
    | <generic_proximity_term>   
    | <custom_proximity_term>   
    |  <weighted_term>   
    }   
    | { ( <contains_search_condition> )   
    { { AND | & } | { AND NOT | &! } | { OR | | } }   
     <contains_search_condition> [ ...n ]   
    }  
  
<simple_term> ::=   
     { word | "phrase" }  
<prefix term> ::=   
     { "word*" | "phrase*" }   
<generation_term> ::=   
     FORMSOF ( { INFLECTIONAL | THESAURUS } , <simple_term> [ ,...n ] )   
  
<generic_proximity_term> ::=   
     { <simple_term> | <prefix_term> } { { { NEAR | ~ }   
     { <simple_term> | <prefix_term> } } [ ...n ] }  
  
<custom_proximity_term> ::=   
  NEAR (   
     {  
        { <simple_term> | <prefix_term> } [ ,...n ]  
     |  
        ( { <simple_term> | <prefix_term> } [ ,...n ] )   
      [, <maximum_distance> [, <match_order> ] ]  
     }  
       )   
  
      <maximum_distance> ::= { integer | MAX }  
      <match_order> ::= { TRUE | FALSE }   
  
<weighted_term> ::=   
     ISABOUT  
    ( { {   
  <simple_term>   
  | <prefix_term>   
  | <generation_term>   
  | <proximity_term>   
  }   
   [ WEIGHT ( weight_value ) ]   
   } [ ,...n ]   
    )  
  
```  
  
## <a name="arguments"></a>인수  
 *table*  
 전체 텍스트 인덱싱된 테이블 이름입니다. *테이블* 은 한 부분, 두 부분, 세 부분 또는 네 부분으로 구성 된 데이터베이스 개체 이름일 수 있습니다. 뷰를 쿼리할 때는 전체 텍스트 인덱싱된 기본 테이블 하나만 포함할 수 있습니다.  
  
 *테이블이* 서버 이름을 지정할 수 없으며 연결 된 서버에 대 한 쿼리에서 사용할 수 없습니다.  
  
 *column_name*  
 전체 텍스트 검색용으로 인덱싱된 하나 이상의 열 이름입니다. 열은 **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** 또는 **varbinary(max)** 형식이 될 수 있습니다.  
  
 *column_list*  
 여러 개의 열을 쉼표로 구분하여 지정할 수 있음을 나타냅니다. *column_list*는 괄호로 묶어야 합니다. *language_term*을 지정하지 않을 경우 *column_list*에 있는 모든 열의 언어가 같아야 합니다.  
  
 \*  
 지정 된 검색 조건을 검색 하는 데 *테이블* 의 모든 전체 텍스트 인덱싱된 열을 사용 하도록 지정 합니다. *language_term*을 지정하지 않을 경우 테이블에 있는 모든 열의 언어가 같아야 합니다.  
  
 LANGUAGE *language_term*  
 쿼리의 일부로 단어 분리, 형태소 분석, 동의어 사전 및 의미 없는 단어 (또는 [중지 단어](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) 제거에 사용할 리소스를 포함 하는 언어입니다. 이 매개 변수는 선택적이며 언어의 LCID(로캘 ID)에 해당하는 문자열, 정수 또는 16진수 값으로 지정할 수 있습니다. *language_term*을 지정할 경우 해당 언어는 검색 조건의 모든 요소에 적용됩니다. 값을 지정하지 않으면 열의 전체 텍스트 언어가 사용됩니다.  
  
 언어가 다른 문서가 단일 열에 BLOB(Binary Large Object)으로 함께 저장된 경우 지정된 문서의 LCID(로캘 ID)에 따라 해당 내용을 인덱싱하는 데 사용할 언어가 결정됩니다. 이러한 열을 쿼리할 때 LANGUAGE** *language_term*을 지정하면 검색 확률을 높일 수 있습니다.  
  
 문자열로 지정 하는 경우 *language_term* 은 [sys.sys언어](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 호환성 보기의 **별칭** 열 값에 해당 합니다.  문자열은 '*language_term*'과 같이 작은따옴표로 묶어야 합니다. 정수로 지정하는 경우 *language_term*은 언어를 식별하는 실제 LCID입니다. 16진수 값으로 지정하는 경우 *language_term*은 0x로 시작하는 16진수 LCID 값입니다. 16진수 값은 앞에 오는 0을 포함하여 8자리 수를 초과할 수 없습니다.  
  
 값이 DBCS(더블바이트 문자 집합) 형식인 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 값을 유니코드로 변환합니다.  
  
 지정된 언어가 잘못되었거나 해당 언어에 해당하는 리소스가 설치되지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오류를 반환합니다. 중립 언어 리소스를 사용하려면 0x0을 *language_term*으로 지정합니다.  
  
 *top_n_by_rank*  
 내림차순으로 가장 높은 *n* 개의 일치 하는 항목만 반환 되도록 지정 합니다. 정수 값 *n*이 지정 된 경우에만 적용 됩니다. *top_n_by_rank* 를 다른 매개 변수와 함께 사용하면 실제로 모든 조건자와 일치하는 행 수보다 적은 수의 행이 반환될 수 있습니다. *top_n_by_rank* 를 사용 하면 관련성이 가장 높은 항목만 회수 하 여 쿼리 성능을 높일 수 있습니다.  
  
 <contains_search_condition>  
 *column_name*에서 검색할 텍스트와 일치 조건을 지정합니다. 검색 조건에 대 한 자세한 내용은 [CONTAINS &#40;transact-sql&#41;](../../t-sql/queries/contains-transact-sql.md)를 참조 하세요.  
  
## <a name="remarks"></a>설명  
 전체 텍스트 조건자와 함수는 단일 테이블에서 작동합니다. 이 사실은 FROM 조건자에 표시됩니다. 여러 테이블을 검색하려면 FROM 절에 조인된 테이블을 사용하여 두 개 이상의 테이블을 합한 결과 집합을 대상으로 검색 작업을 수행합니다.  
  
 반환 된 테이블에는 전체 텍스트 키 값을 포함 하는 **key** 라는 열이 있습니다. 각 전체 텍스트 인덱싱된 테이블에는 값이 고유 하도록 보장 되는 열이 있고 **키** 열에 반환 된 값은 contains 검색 조건에 지정 된 선택 조건과 일치 하는 행의 전체 텍스트 키 값입니다. OBJECTPROPERTYEX 함수에서 가져온 **TableFulltextKeyColumn** 속성은이 고유 키 열의 id를 제공 합니다. 전체 텍스트 인덱스의 전체 텍스트 키와 연결 된 열의 ID를 가져오려면 **fulltext_indexes**를 사용 합니다. 자세한 내용은 [fulltext_indexes &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)을 참조 하십시오.  
  
 원래 테이블에서 원하는 행을 얻으려면 CONTAINSTABLE 행과 조인을 지정합니다. 일반적인 SELECT 문의 FROM 절에서 CONTAINSTABLE을 사용한 예는 다음과 같습니다.  
  
```  
SELECT select_list  
FROM table AS FT_TBL INNER JOIN  
   CONTAINSTABLE(table, column, contains_search_condition) AS KEY_TBL  
   ON FT_TBL.unique_key_column = KEY_TBL.[KEY];  
```  
  
 CONTAINSTABLE에서 생성 된 테이블에는 **RANK**라는 열이 포함 되어 있습니다. **RANK** 열은 각 행이 선택 조건과 일치 하는 정도를 나타내는 값 (0에서 1000 사이)입니다. 이러한 등급 값은 대개 SELECT 문에서 다음과 같이 사용됩니다.  
  
-   ORDER BY 절에서 등급 값이 가장 높은 행을 테이블의 첫 번째 행으로 반환합니다.  
  
-   선택 목록에서 각 행에 할당된 등급 값을 봅니다.  
  
## <a name="permissions"></a>사용 권한  
 테이블이나 참조되는 테이블의 열에 대해 SELECT 권한이 있는 사용자만 실행 권한이 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-simple-example"></a>A. 간단한 예  
 다음 예에서는 3 개의 군을 나열 하 고 플래그에 색을 나열 하는 두 개의 열로 이루어진 간단한 테이블을 만들고 채웁니다. 이 예제에서는 테이블에 대 한 전체 텍스트 카탈로그 및 인덱스를 만들고 채웁니다. 그런 다음 **CONTAINSTABLE** 구문을 보여 줍니다. 이 예에서는 검색 값이 여러 번 충족 될 때 순위 값이 증가 하는 방식을 보여 줍니다. 마지막 쿼리에서 녹색 및 검정을 모두 포함 하는 탄자니아는 쿼리 된 색 중 하나만 포함 하는 이탈리아 보다 더 높은 순위를 갖습니다.  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM CONTAINSTABLE (Flags, FlagColors, 'Green') ORDER BY RANK DESC;  
SELECT * FROM CONTAINSTABLE (Flags, FlagColors, 'Green or Black') ORDER BY RANK DESC;  
```  
  
### <a name="b-returning-rank-values"></a>B. 순위 값 반환  
 다음 예에서는 "frame," "wheel" 또는 "tire"라는 단어가 포함된 모든 제품 이름을 검색하며 각 단어에는 다른 가중치가 지정됩니다. 선택 조건과 일치하여 반환된 각 행에 대해 상대적인 일치 정도(등급 값)가 표시되며 등급 값이 가장 높은 행이 제일 먼저 반환됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Name, KEY_TBL.RANK  
    FROM Production.Product AS FT_TBL   
        INNER JOIN CONTAINSTABLE(Production.Product, Name,   
        'ISABOUT (frame WEIGHT (.8),   
        wheel WEIGHT (.4), tire WEIGHT (.2) )' ) AS KEY_TBL  
            ON FT_TBL.ProductID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
### <a name="c-returning-rank-values-greater-than-a-specified-value"></a>C. 지정된 값보다 큰 등급 값 반환  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상|  
  
 다음 예에서는 NEAR를 사용하여 `bracket` 테이블에서 서로 가까이 있는 "`reflector`"과 "`Production.Document`"를 검색합니다. 등급 값이 50 이상인 행만 반환됩니다.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
> [!NOTE]  
>  전체 텍스트 쿼리에서 정수를 최대 거리로 지정하지 않은 경우 거리가 100개의 논리적 용어보다 항목만 포함하는 문서는 NEAR 요구 사항을 충족하지 않으며 순위가 0이 됩니다.  
  
### <a name="d-returning-top-5-ranked-results-using-top_n_by_rank"></a>D. top_n_by_rank를 사용하여 상위 5개 결과 반환  
 다음 예에서는 `Description` 열에 "light"나 "lightweight"라는 단어와 근접한 "aluminum"이라는 단어가 포함된 상위 5개 제품에 대한 설명을 반환합니다.  
  
```  
USE AdventureWorks2012;  
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
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY];  
GO  
```  
  
 `GO`  
  
### <a name="e-specifying-the-language-argument"></a>E. LANGUAGE 인수 지정  
 다음 예에서는 `LANGUAGE` 인수를 사용하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      LANGUAGE N'English',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY];  
GO  
```  
  
> [!NOTE]  
>  Top_n_by_rank를 사용 하는 경우 언어 *language_term* argumentis 필요 하지 않습니다 *.*  
  
## <a name="see-also"></a>참고 항목  
 [RANK를 사용 하 여 검색 결과 제한](../../relational-databases/search/limit-search-results-with-rank.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [전체 텍스트 검색 쿼리 만들기&#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS&#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  
