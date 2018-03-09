---
title: "(Transact SQL)를 포함 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONTAINS_TSQL
- CONTAINS
dev_langs:
- TSQL
helpviewer_keywords:
- precise or fuzzy (less precise) matches [full-text search]
- CONTAINS predicate (Transact-SQL)
- conditions [SQL Server], CONTAINS
- fuzzy (less precise) word or phrase search [full-text search]
- word weighting values [full-text search]
- word searches [full-text search]
- weighted values [full-text search]
- LANGUAGE option
- word inflectionally generated from another [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- word near another word search [full-text search]
- full-text search [SQL Server], searching on a property
- proximity searches [full-text search]
- less precise (fuzzy) searches [full-text search]
- property searching [SQL Server], searching on a property
- inflectional forms [full-text search]
- prefix searches [full-text search]
ms.assetid: 996c72fc-b1ab-4c96-bd12-946be9c18f84
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 81b231ce95ae1b87bbda2f2fd786d12cb709e9fe
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="contains-transact-sql"></a>CONTAINS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 특정 단어 또는 구와 정확히 일치하거나 비슷하게 일치하는 단어를 검색하거나 서로 근접한 단어를 검색하거나 가중치 검색을 수행합니다. CONTAINS는에서 사용 되는 조건자는 [WHERE 절](../../t-sql/queries/where-transact-sql.md) 의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 수행 하기 위해 SELECT 문의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색 전체 텍스트 인덱싱된 열의 문자 기반 데이터 형식이 포함 합니다.  
  
 CONTAINS는 다음을 검색할 수 있습니다.  
  
-   단어나 구  
  
-   단어나 구의 접두사  
  
-   다른 단어에 근접한 단어  
  
-   다른 단어에서 어미를 변화하여 생성된 단어(예: drive라는 단어는 drives, drove, driving, driven의 어간임)  
  
-   동의어 사전을 사용할 때 다른 단어의 동의어인 단어(예: "metal"이라는 단어에는 "aluminum" 및 "steel" 같은 동의어가 있을 수 있음)  
  
 전체 텍스트 검색에서 지원 되는 형식에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 참조 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)합니다.  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CONTAINS (   
     {   
        column_name | ( column_list )   
      | *   
      | PROPERTY ( { column_name }, 'property_name' )    
     }   
     , '<contains_search_condition>'  
     [ , LANGUAGE language_term ]  
   )   
  
<contains_search_condition> ::=   
  {   
      <simple_term>   
    | <prefix_term>   
    | <generation_term>   
    | <generic_proximity_term>   
    | <custom_proximity_term>   
    | <weighted_term>   
    }   
  |   
    { ( <contains_search_condition> )   
        [ { <AND> | <AND NOT> | <OR> } ]   
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
        { <simple_term> | <prefix_term> } [ ,…n ]  
     |  
        ( { <simple_term> | <prefix_term> } [ ,…n ] )   
      [, <maximum_distance> [, <match_order> ] ]  
     }  
       )   
  
      <maximum_distance> ::= { integer | MAX }  
      <match_order> ::= { TRUE | FALSE }   
  
<weighted_term> ::=   
  ISABOUT   
   ( {   
        {   
          <simple_term>   
        | <prefix_term>   
        | <generation_term>   
        | <proximity_term>   
        }   
      [ WEIGHT ( weight_value ) ]   
      } [ ,...n ]   
   )   
  
<AND> ::=   
  { AND | & }  
  
<AND NOT> ::=   
  { AND NOT | &! }  
  
<OR> ::=   
  { OR | | }  
  
```  
  
## <a name="arguments"></a>인수  
 *column_name*  
 FROM 절에 지정된 테이블에 대한 전체 텍스트 인덱싱된 열의 이름입니다. 열 형식이 될 수 있습니다 **char**, **varchar**, **nchar**, **nvarchar**, **텍스트**, **ntext**, **이미지**, **xml**, **varbinary**, 또는 **varbinary (max)**합니다.  
  
 *column_list*  
 쉼표로 구분된 두 개 이상의 열을 지정합니다. *column_list* 괄호로 묶어야 합니다. 하지 않는 한 *language_term* 지정 된 언어의 모든 열 *column_list* 동일 해야 합니다.  
  
 \*  
 쿼리를 지정된 된 검색 조건에 대 한 FROM 절에 지정 된 테이블의 모든 전체 텍스트 인덱싱된 열을 검색 하도록 지정 합니다. CONTAINS 절의 열은 전체 텍스트 인덱스가 있는 단일 테이블에서 가져와야 합니다. 하지 않는 한 *language_term* 지정, 테이블의 모든 열의 언어가 동일 해야 합니다.  
  
 속성 ( *column_name* , '*property_name*')  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 지정한 검색 조건을 검색할 문서 속성을 지정합니다.  
  
> [!IMPORTANT]  
>  행을 반환 하는 쿼리에 대 한 *property_name* ज 검색 속성 목록이 전체 텍스트 인덱스 및 전체 텍스트 인덱스에 대 한 속성 관련 항목 있어야 *property_name*합니다. 자세한 내용은 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하세요.  
  
 LANGUAGE *language_term*  
 단어 분리, 형태소 분석, 동의어 사전 확장 및 대체 작업 및 의미 없는 단어에 사용할 언어 (또는 [중지 단어](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md))는 쿼리의 일환으로 제거 합니다. 이 매개 변수는 선택 사항입니다.  
  
 언어가 다른 문서가 단일 열에 BLOB(Binary Large Object)로 함께 저장된 경우 지정된 문서의 LCID(로캘 ID)에 따라 해당 내용을 인덱싱하는 데 사용할 언어가 결정됩니다. 이러한 열을 쿼리할 때 사용할 언어를 지정 하 *language_term* 가장 잘 맞는의 확률을 높일 수 있습니다.  
  
 *language_term* 문자열, 정수 또는 16 진수 값에 해당 하는 언어의 LCID로 지정할 수 있습니다. 경우 *language_term* , 지정한 언어는 검색 조건의 모든 요소에 적용 됩니다. 값을 지정하지 않으면 열의 전체 텍스트 언어가 사용됩니다.  
  
 문자열로 지정 하는 경우 *language_term* 에 해당 하는 **별칭** 열 값에는 [sys.syslanguages&#40; Transact SQL &#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 호환성 보기. 와 같이 하나의 따옴표로 묶어야 합니다 문자열 '*language_term*'. 정수로 지정 된 경우 *language_term* 는 언어를 식별 하는 실제 LCID입니다. 16 진수 값으로 지정 하는 경우 *language_term* 된 LCID의 16 진수 값은 0x 시작 합니다. 16진수 값은 선행 0을 포함하여 8자리 수를 초과할 수 없습니다.  
  
 더블 바이트 문자 집합 (DBCS) 형식인 경우에 값이 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 유니코드로 변환 합니다.  
  
 지정된 언어가 잘못되었거나 해당 언어에 해당하는 리소스가 설치되지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오류를 반환합니다. 중립 언어 리소스를 사용 하려면 0x0 지정 *language_term*합니다.  
  
 \<*contains_search_condition*>  
 검색할 텍스트를 지정 *column_name* 과 일치 하는 항목에 대 한 상태입니다.  
  
*\<contains_search_condition >* 은 **nvarchar**합니다. 암시적 변환은 다른 문자 데이터 형식이 입력으로 사용될 때 발생합니다. 큰 문자열 데이터 형식 nvarchar (max) 및 varchar (max)를 사용할 수 없습니다. 다음 예에서는 `@SearchWord`로 정의된 `varchar(30)` 변수로 인해 `CONTAINS` 조건자에서 암시적 변환이 발생합니다.
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 "매개 변수 스니핑" 변환에서 작동 하지 않고, 사용 하 여 **nvarchar** 성능 향상을 위해 합니다. 예제에서는 선언 `@SearchWord` 으로 `nvarchar(30)`합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 최적화되지 않은 계획이 생성되는 경우 OPTIMIZE FOR 쿼리 힌트를 사용할 수도 있습니다.  
  
 *word*  
 공백이나 문장 부호가 포함되지 않은 문자열입니다.  
  
 *phrase*  
 각 단어 사이에 공백이 포함된 하나 이상의 단어입니다.  
  
> [!NOTE]  
>  몇몇 아시아 지역의 언어로 작성된 경우처럼 일부 언어에는 각 단어 사이에 공백이 없는 하나 이상의 단어로 구성된 구가 있을 수 있습니다.  
  
\<simple_term>  
단어나 구가 정확하게 일치하는 항목을 지정합니다. 유효한 단순 단어의 예로는 "blue berry", blueberry, "Microsoft SQL Server" 등이 있습니다. 구는 큰따옴표("")로 묶어야 합니다. 이 구에서의 단어에 지정 된 대로 동일한 순서로 나타나야 합니다  *\<contains_search_condition >* 데이터베이스 열에 표시 된 대로 합니다. 단어나 구에서 문자를 검색할 때는 대/소문자를 구분하지 않습니다. 의미 없는 단어 (또는 [중지 단어](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) (예: a를 또는)에서 전체 텍스트 인덱싱된 열에에서 저장 되지 않습니다는 전체 텍스트 인덱스 합니다. 단일 단어 검색에 의미 없는 단어가 사용되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 쿼리에 의미 없는 단어만 포함되어 있다는 오류 메시지를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 \Mssql\Binn\FTERef 디렉터리에 의미 없는 단어 표준 목록이 포함되어 있습니다.  
  
 문장 부호는 무시됩니다. 따라서 `CONTAINS(testing, "computer failure")`는 "Where is my computer? Failure to find it would be expensive."라는 값을 가진 행을 검색합니다. 단어 분리기 동작에 대 한 자세한 내용은 참조 하십시오. [관리 단어 분리기와 형태소 분석기 검색에 대 한 구성 및](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)합니다.  
  
 \<prefix_term>  
 지정한 텍스트로 시작하는 단어 또는 구를 검색하도록 지정합니다. 접두사 단어 큰따옴표로 묶습니다 ("")는 별표를 추가 하 고 (\*) 끝 따옴표가 하기 전에 하기 전에 단순 단어로 시작 하는 모든 텍스트를 지정 하는 별표 일치 합니다. 절은 `CONTAINS (column, '"text*"')`와 같이 지정해야 합니다. 별표는 단어나 구에 포함된 어근의 문자를 개수에 관계없이 검색합니다. 텍스트와 별표를 큰따옴표로 구분하지 않으면 조건자가 `CONTAINS (column, 'text*')`를 읽고 전체 텍스트 검색에서 별표를 문자로 간주하여 `text*`와 정확하게 일치하는 텍스트를 검색합니다. 전체 텍스트 엔진은 단어를 별표를 찾지 못합니다 (\*) 단어 분리기 일반적으로 이러한 문자를 무시 하기 때문에 문자입니다.  
  
 때  *\<접두어 >* 는 구, 구에 포함 된 각 단어는 별도 접두사로 간주 됩니다. 따라서 접두사 단어 "local wine*"을 지정하는 쿼리는 "local winery", "locally wined and dined" 등의 텍스트가 포함된 모든 행을 검색합니다.  
  
 \<generation_term>  
 포함된 단순 단어에 검색할 원래 단어에서 변형된 단어가 포함된 경우 단어를 검색하도록 지정합니다.  
  
 INFLECTIONAL  
 지정된 단순 단어에 언어별 형태소 분석기를 사용하도록 지정합니다. 형태소 분석기 동작은 각 언어의 형태소 분석 규칙에 따라 정의됩니다. 중립 언어에는 관련된 형태소 분석기가 없습니다. 쿼리할 열의 열 언어는 원하는 형태소 분석기를 참조하는 데 사용됩니다. 경우 *language_term* 지정 된 형태소 분석기를 해당 언어가 사용 됩니다.  
  
 지정 된  *\<단순 어 >* 내에서 한  *\<파생어 >* 명사와 동사와 일치 하지 것입니다.  
  
 THESAURUS  
 열의 전체 텍스트 언어 또는 쿼리에 지정된 언어에 해당되는 동의어 사전이 사용되도록 지정합니다. 가장 긴 패턴 또는 패턴을는  *\<단순 어 >* 동의어 사전에 대해 일치 하 고 확장 하거나 원래 패턴을 대체 하도록 추가 단어가 생성 됩니다. 전체 또는 일부에 대 한 일치 하는 항목이 없는 경우는  *\<단순 어 >*, 일치 하지 않는 부분으로 처리 됩니다는 *단순 어*합니다. 전체 텍스트 검색 동의어 사전에 대 한 자세한 내용은 참조 하십시오. [전체 텍스트 검색에 대 한 동의어 사전 파일 관리 및 구성](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)합니다.  
  
 \<generic_proximity_term>  
 검색 대상 문서에 있어야 하는 단어 또는 구를 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하는 것이 좋습니다 \<custom_proximity_term > 합니다.  
  
 NEAR | ~  
 일치 항목이 반환되려면 NEAR 또는 ~ 연산자의 양쪽에 있는 단어나 구가 문서에 있어야 함을 나타냅니다. 두 개의 검색 단어를 지정해야 합니다. 한 단어 또는 구를 큰따옴표로 구분 되는 지정한 검색 단어 될 수 있습니다 ("*구*").  
  
 `a NEAR b NEAR c` 또는 `a ~ b ~ c`와 같이 근접 단어를 여러 개 연결할 수 있습니다. 일치 항목이 반환되려면 연결된 근접 단어가 모두 해당 문서에 있어야 합니다.  
  
 예를 들어 `CONTAINS(*column_name*, 'fox NEAR chicken')` 및 `CONTAINSTABLE(*table_name*, *column_name*, 'fox ~ chicken')` 은 둘 다 반환 모든 문서에서 "fox"와 "chicken"을 모두 포함 하는 지정된 된 열입니다. 또한 CONTAINSTABLE은 "fox" 및 "chicken"의 근접 정도에 따라 각 문서의 순위를 반환합니다. 예를 들어 문서에 "The fox ate the chicken"이라는 문장이 있으면 다른 문서에 비해 단어가 서로 가까이 있으므로 문서 순위가 높아집니다.  
  
 일반적인 근접 단어에 대 한 자세한 내용은 참조 [단어 검색 NEAR 사용 하 여를](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)합니다.  
  
 \<custom_proximity_term>  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 일치시킬 단어나 구를 지정하고 선택적으로 검색 단어 사이에 허용할 최대 거리를 지정합니다. 지정 하는 정확한 순서에 검색 용어를 찾을 수 있어야 지정할 수도 있습니다 (\<과 >).  
  
 한 단어 또는 구를 큰따옴표로 구분 되는 지정한 검색 단어 될 수 있습니다 ("*구*"). 일치 항목이 반환되려면 지정한 단어가 모두 해당 문서에 있어야 합니다. 두 단어 이상을 지정해야 합니다. 최대 검색 단어 수는 64입니다.  
  
 기본적으로 사용자 지정 근접 단어는 지정한 단어 사이의 거리 및 순서와 관계없이 해당 단어가 포함된 행을 모두 반환합니다. 예를 들어 다음 쿼리를 일치시키려면 문서에 `term1` 및 "`term3 term4`"이 순서와 위치에 관계없이 포함되어야 합니다.  
  
```  
CONTAINS(column_name, 'NEAR(term1,"term3 term4")')  
```  
  
 선택적 매개 변수는 다음과 같습니다.  
  
 \<maximum_distance>  
 문자열이 일치 항목으로 처리될 수 있는 순서로 문자열 처음과 끝에 검색 단어 사이에 허용되는 최대 거리를 지정합니다.  
  
 *integer*  
 0에서 4294967295 사이의 양의 정수를 지정합니다. 이 값은 지정한 추가 검색 단어를 제외한 처음과 마지막 검색 단어 사이에 올 수 있고 검색 대상이 아닌 단어 수를 제어합니다.  
  
 예를 들어 다음 쿼리를 검색 `AA` 및 `BB`, 어떤 순서로 든 최대 거리 5 내에서.  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB),5)')  
```  
  
 문자열 `AA one two three four five BB` 일치 하는 것입니다. 다음 예제에서는 쿼리에서 지정 검색어를 3 개에 대 한 `AA`, `BB`, 및 `CC` 최대 거리 5 내:  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB,CC),5)')  
```  
  
 이 쿼리는 전체 거리가 5인 다음 문자열을 일치시킵니다.  
  
 `BB   one two   CC   three four five A  A`  
  
 내부 용어를 검색 하는 알림 `CC`, 계산 되지 않습니다.  
  
 **MAX**  
 지정된 단어 사이의 거리와 관계없이 해당 단어가 포함된 행을 모두 반환합니다. 기본값입니다.  
  
 \<match_order>  
 검색 쿼리에서 반환하도록 지정한 순서로 단어가 나올지 여부를 지정합니다. 지정 하려면 \<과 >을 지정 해야 \<maximum_distance > 합니다.  
  
 \<과 >는 다음 값 중 하나를 사용 합니다.  
  
 **TRUE**  
 단어에 지정한 순서를 적용합니다. 예를 들어 `NEAR(A,B)`는 `A … B`에만 일치합니다.  
  
 **FALSE**  
 지정한 순서를 무시합니다. 예를 들어 `NEAR(A,B)`는 `A … B` 및 `B … A`와 모두 일치합니다.  
  
 기본값입니다.  
  
 예를 들어 다음 근접 단어는 거리와 관계없이 지정한 순서로 "`Monday`", "`Tuesday`" 및 "`Wednesday`" 단어를 검색합니다.  
  
```  
CONTAINS(column_name, 'NEAR ((Monday, Tuesday, Wednesday), MAX, TRUE)')  
```  
  
 사용자 지정 근접 단어를 사용 하는 방법에 대 한 자세한 내용은 참조 [단어 검색 NEAR 사용 하 여를](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)합니다.  
  
 \<weighted_term>  
 쿼리에서 반환된 결과 행이 단어 및 구 목록과 일치하고 선택적으로 가중치 값이 지정되도록 합니다.  
  
 ISABOUT  
 지정 된  *\<가중치 어 >* 키워드입니다.  
  
 WEIGHT(*weight_value*)  
 0.0에서 1.0 사이의 숫자로 가중치를 지정합니다. 각 구성 요소에  *\<가중치 어 >* 포함 될 수 있습니다는 *로*합니다. *로* 쿼리의 다양 한 부분에는 쿼리와 일치 하는 각 행에 할당 된 등급 값에 영향을 변경할 수 있는 방법이 있습니다. 가중치 CONTAINS 쿼리는 하지만의 영향을 미치는 순위 가중치의 결과는 영향을 주지 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 쿼리 합니다.  
  
> [!NOTE]  
>  소수 구분 기호는 운영 체제 로캘에 관계없이 항상 마침표입니다.  
  
 { AND | & } | { AND NOT | &! } | { OR | | }  
 두 개의 포함 검색 조건 간에 논리적 연산을 지정합니다.  
  
 { AND | & }  
 두 개의 포함 검색 조건이 모두 충족되어야 일치한다는 것을 나타냅니다. AND 키워드 대신 앰퍼샌드 기호(&)를 사용하여 AND 연산자를 나타낼 수도 있습니다.  
  
 {아닌 | &! }  
 두 번째 검색 조건이 일치하지 않아야 한다는 것을 나타냅니다. AND NOT 키워드 대신 앰퍼샌드 다음에 느낌표 기호(&!)를 사용하여 AND NOT 연산자를 나타낼 수도 있습니다.  
  
 { OR | | }  
 두 개의 포함 검색 조건 중 하나가 충족되어야 일치한다는 것을 나타냅니다. OR 키워드 대신 막대 기호(|)를 사용하여 OR 연산자를 나타낼 수도 있습니다.  
  
 때  *\<contains_search_condition >* 괄호로 묶인 그룹, 괄호로이 묶인 그룹이 먼저 계산 됩니다. 괄호로 묶인 그룹을 평가한 후 포함 검색 조건에 논리 연산자를 사용할 때 다음 규칙이 적용됩니다.  
  
-   AND보다 NOT이 먼저 적용됩니다.  
  
-   AND NOT과 같이 NOT은 AND 다음에만 올 수 있으며 OR NOT 연산자는 허용되지 않습니다. NOT은 첫 번째 단어 앞에 지정할 수 없습니다. 예를 들어 `CONTAINS (mycolumn, 'NOT "phrase_to_search_for" ' )`는 유효하지 않습니다.  
  
-   OR보다 AND가 먼저 적용됩니다.  
  
-   동일한 유형의 부울 연산자(AND, OR)는 결합성을 가지므로 어떤 순서로든 적용할 수 있습니다.  
  
 *n*  
 여러 CONTAINS 검색 조건과 용어를 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 전체 텍스트 조건자와 함수는 단일 테이블에서 작동합니다. 이 사실은 FROM 조건자에 표시됩니다. 여러 테이블을 검색하려면 FROM 절에 조인된 테이블을 사용하여 두 개 이상의 테이블을 합한 결과 집합을 대상으로 검색 작업을 수행합니다.  
  
 전체 텍스트 조건자에서 허용 되지 않습니다는 [OUTPUT 절](../../t-sql/queries/output-clause-transact-sql.md) 데이터베이스 호환성 수준이 100으로 설정 된 경우.  
  
## <a name="querying-remote-servers"></a>원격 서버 쿼리  
 네 부분으로 된 이름을 사용 하 여 contains에서 또는 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 조건자 전체 텍스트 쿼리 인덱싱된 연결 된 서버의 대상 테이블의 열입니다. 원격 서버에서 전체 텍스트 쿼리를 받도록 준비하려면 원격 서버의 대상 테이블 및 열에 대한 전체 텍스트 인덱스를 만든 다음 원격 서버를 연결된 서버로 추가합니다.  
  
## <a name="comparison-of-like-to-full-text-search"></a>LIKE와 전체 텍스트 검색 비교  
 전체 텍스트 검색과 달리 [LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 조건자는 문자 패턴에 대해서만 적용됩니다. 또한 LIKE 조건자는 서식 있는 이진 데이터를 쿼리하는 데 사용할 수도 없습니다. 특히 구조화되지 않은 많은 텍스트 데이터에 대한 LIKE 쿼리는 동일한 데이터에 대한 전체 텍스트 쿼리보다 훨씬 느립니다. 수백만 개의 텍스트 데이터 행에 대한 LIKE 쿼리는 결과가 반환되기까지 몇 분이 걸릴 수 있지만 동일한 데이터에 대한 전체 텍스트 쿼리는 반환되는 행 수와 해당 크기에 따라 몇 초 내에 완료됩니다. LIKE는 전체 테이블의 단순 패턴 스캔만 수행한다는 점도 고려하십시오. 반대로 전체 텍스트 쿼리는 언어를 인식하며 인덱스 및 쿼리 시 중지 단어 필터링, 동의어 사전 및 활용 형태상의 확장과 같은 특정 변환을 적용합니다. 이러한 변환을 통해 전체 텍스트 쿼리의 재호출 및 최종 결과 순위가 향상됩니다.  
  
## <a name="querying-multiple-columns-full-text-search"></a>여러 열 쿼리(전체 텍스트 검색)  
 검색할 열 목록을 지정하여 여러 열을 쿼리할 수 있습니다. 열은 동일한 테이블에 있어야 합니다.  
  
 다음 CONTAINS 쿼리 용어를 검색 하는 예를 들어 `Red` 에 `Name` 및 `Color` 의 열은 `Production.Product` 테이블의는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스.  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Name, Color   
FROM Production.Product  
WHERE CONTAINS((Name, Color), 'Red');  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-using-contains-with-simpleterm"></a>1. CONTAINS를 사용 하 여 \<단순 어 >  
 다음 예에서는 가격이 `$80.99` 이고 `Mountain`이라는 단어가 포함된 모든 제품을 검색합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain');  
GO  
```  
  
### <a name="b-using-contains-and-phrase-with-simpleterm"></a>2. CONTAINS 및 구 사용를 사용 하 여 \<단순 어 >  
 다음 예에서는 `Mountain`이나 `Road`라는 구가 포함된 모든 제품을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' Mountain OR Road ')  
GO  
```  
  
### <a name="c-using-contains-with-prefixterm"></a>3. CONTAINS를 사용 하 여 \<접두어 >  
 다음 예에서는 `Name` 열에 접두사 chain으로 시작하는 단어가 하나 이상인 모든 제품 이름을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' "Chain*" ');  
GO  
```  
  
### <a name="d-using-contains-and-or-with-prefixterm"></a>4. CONTAINS를 사용 하 여 or \<접두어 >  
 다음 예에서는 접두사가 `chain` 또는 `full`인 문자열을 포함하는 모든 범주 설명을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, '"chain*" OR "full*"');  
GO  
```  
  
### <a name="e-using-contains-with-proximityterm"></a>5. CONTAINS를 사용 하 여 \<근접어 >  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 검색 하 여 해당는 `Production.ProductReview` 테이블 이라는 단어가 포함 된 모든 설명을 `bike` 단어의 10 단어 이내로 "`control`" 및 지정 된 순서로 (즉, "`bike`"앞 에"`control`").  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments , 'NEAR((bike,control), 10, TRUE)');  
GO  
```  
  
### <a name="f-using-contains-with-generationterm"></a>6. CONTAINS를 사용 하 여 \<파생어 >  
 다음 예에서는 riding, ridden 등 `ride`에서 파생된 단어가 있는 모든 제품을 검색합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, ' FORMSOF (INFLECTIONAL, ride) ');  
GO  
```  
  
### <a name="g-using-contains-with-weightedterm"></a>7. CONTAINS를 사용 하 여 \<가중치 어 >  
 다음 예에서는 `performance`, `comfortable` 또는 `smooth` 단어가 포함된 모든 제품 이름을 검색하며 각 단어에는 다른 가중치가 지정됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, 'ISABOUT (performance weight (.8),   
comfortable weight (.4), smooth weight (.2) )' );  
GO  
```  
  
### <a name="h-using-contains-with-variables"></a>8. 변수에 CONTAINS 사용  
 다음 예에서는 특정 검색 용어 대신 변수를 사용합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'Performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
GO  
```  
  
### <a name="i-using-contains-with-a-logical-operator-and"></a>9. 논리 연산자(AND)에 CONTAINS 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 ProductDescription 테이블을 사용합니다. 쿼리는 CONTAINS 조건자를 사용 하 여 설명 ID가 5 하지 설명을 검색와 두 단어 포함 `Aluminum` 와 단어가 `spindle`합니다. 검색 조건에는 AND 부울 연산자가 사용됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'Aluminum AND spindle');  
GO  
```  
  
### <a name="j-using-contains-to-verify-a-row-insertion"></a>10. CONTAINS를 사용하여 행 삽입 확인  
 다음 예에서는 SELECT 하위 쿼리 내에 CONTAINS를 사용합니다. 이 쿼리는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용하여 특정 주기에 대한 ProductReview 테이블의 모든 설명 값을 얻습니다. 검색 조건에는 AND 부울 연산자가 사용됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Production.ProductReview   
  (ProductID, ReviewerName, EmailAddress, Rating, Comments)   
VALUES  
  (780, 'John Smith', 'john@fourthcoffee.com', 5,   
'The Mountain-200 Silver from AdventureWorks2008 Cycles meets and exceeds expectations. I enjoyed the smooth ride down the roads of Redmond');  
  
-- Given the full-text catalog for these tables is Adv_ft_ctlg,   
-- with change_tracking on so that the full-text indexes are updated automatically.  
WAITFOR DELAY '00:00:30';     
-- Wait 30 seconds to make sure that the full-text index gets updated.  
  
SELECT r.Comments, p.Name  
FROM Production.ProductReview AS r  
JOIN Production.Product AS p   
    ON r.ProductID = p.ProductID  
    AND r.ProductID = (SELECT ProductID  
FROM Production.ProductReview  
WHERE CONTAINS (Comments,   
    ' AdventureWorks2008 AND   
    Redmond AND   
    "Mountain-200 Silver" '));  
GO  
```  
  
### <a name="k-querying-on-a-document-property"></a>11. 문서 속성 쿼리  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
 다음 쿼리는 `Title` 테이블의 `Document` 열에서 인덱싱된 속성 `Production.Document`을 검색합니다. 쿼리는 `Title` 속성에 `Maintenance` 또는 `Repair` 문자열이 포함된 문서만 반환합니다.  
  
> [!NOTE]  
>  속성 검색에서 행을 반환하기 위해서는 인덱싱하는 동안 열을 구문 분석하는 필터가 지정한 속성을 추출해야 합니다. 또한 지정한 테이블의 전체 텍스트 인덱스가 속성을 포함하도록 구성되어 있어야 합니다. 자세한 내용은 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하세요.  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Document 
FROM Production.Document  
WHERE CONTAINS(PROPERTY(Document,'Title'), 'Maintenance OR Repair');  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [전체 텍스트 검색 시작](../../relational-databases/search/get-started-with-full-text-search.md)   
 [전체 텍스트 카탈로그 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [전체 텍스트 카탈로그 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [전체 텍스트 검색 쿼리 만들기&#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
