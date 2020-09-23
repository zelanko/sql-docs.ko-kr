---
title: CONTAINS (Transact-SQL) | Microsoft Docs
description: CONTAINS 언어 요소의 Transact-SQL 참조입니다. 다른 식에서 단어 또는 구를 검색하는 데 사용됩니다.
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 04e11f27d26a7979dfc84b29d7c7de1b02eb02ab
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115428"
---
# <a name="contains-transact-sql"></a>CONTAINS(Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 특정 단어 또는 구와 정확히 일치하거나 비슷하게 일치하는 단어를 검색하거나 서로 근접한 단어를 검색하거나 가중치 검색을 수행합니다. CONTAINS는 문자 기반 데이터 형식이 포함된 전체 텍스트 인덱싱된 열에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색을 수행하기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 문의 [WHERE 절](../../t-sql/queries/where-transact-sql.md)에 사용되는 조건자입니다.  
  
 CONTAINS는 다음을 검색할 수 있습니다.  
  
-   단어나 구  
  
-   단어나 구의 접두사  
  
-   다른 단어에 근접한 단어  
  
-   다른 단어에서 어미를 변화하여 생성된 단어(예: drive라는 단어는 drives, drove, driving, driven의 어간임)  
  
-   동의어 사전을 사용할 때 다른 단어의 동의어인 단어(예: "metal"이라는 단어에는 "aluminum" 및 "steel" 같은 동의어가 있을 수 있음)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 전체 텍스트 검색 형식에 대한 자세한 내용은 [전체 텍스트 검색이 있는 쿼리](../../relational-databases/search/query-with-full-text-search.md)를 참조하세요.  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
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
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *column_name*  
 FROM 절에 지정된 테이블에 대한 전체 텍스트 인덱싱된 열의 이름입니다. 열은 **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** 또는 **varbinary(max)** 형식이 될 수 있습니다.  
  
 *column_list*  
 쉼표로 구분된 두 개 이상의 열을 지정합니다. *column_list*는 괄호로 묶어야 합니다. *language_term*을 지정하지 않을 경우 *column_list*에 있는 모든 열의 언어가 같아야 합니다.  
  
 \*  
 지정된 검색 조건에 대해 쿼리가 FROM 절에 지정된 테이블에서 전체 텍스트 인덱싱된 열을 모두 검색하도록 지정합니다. CONTAINS 절의 열은 전체 텍스트 인덱스가 있는 단일 테이블에서 가져와야 합니다. *language_term*을 지정하지 않을 경우 테이블에 있는 모든 열의 언어가 같아야 합니다.  
  
 PROPERTY ( *column_name* , '*property_name*')  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 
  
 지정한 검색 조건을 검색할 문서 속성을 지정합니다.  
  
> [!IMPORTANT]  
>  쿼리에서 행을 반환하려면 *property_name*이 전체 텍스트 인덱스의 검색 속성 목록에 지정되고 *property_name*의 속성별 항목이 전체 텍스트 인덱스에 포함되어야 합니다. 자세한 내용은 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하세요.  
  
 LANGUAGE *language_term*  
 단어 분리, 형태소 분석, 동의어 사전 확장 및 대체, 의미 없는 단어 또는 [중지 단어](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) 제거를 위해 쿼리의 일부로 사용할 언어입니다. 이 매개 변수는 선택 사항입니다.  
  
 언어가 다른 문서가 단일 열에 BLOB(Binary Large Object)로 함께 저장된 경우 지정된 문서의 LCID(로캘 ID)에 따라 해당 내용을 인덱싱하는 데 사용할 언어가 결정됩니다. 이러한 열을 쿼리할 때 LANGUAGE *language_term*을 지정하면 검색 확률을 높일 수 있습니다.  
  
 *language_term*은 특정 언어의 LCID에 해당하는 문자열, 정수 또는 16진수 값으로 지정할 수 있습니다. *language_term*을 지정할 경우 해당 언어는 검색 조건의 모든 요소에 적용됩니다. 값을 지정하지 않으면 열의 전체 텍스트 언어가 사용됩니다.  
  
 문자열로 지정하는 경우 *language_term*은 [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 호환성 뷰의 **alias** 열 값에 해당합니다. 문자열은 '*language_term*'과 같이 작은따옴표로 묶어야 합니다. 정수로 지정하는 경우 *language_term*은 언어를 식별하는 실제 LCID입니다. 16진수 값으로 지정하는 경우 *language_term*은 0x로 시작하는 16진수 LCID 값입니다. 16진수 값은 앞에 오는 0을 포함하여 8자리 수를 초과할 수 없습니다.  
  
 값이 DBCS(더블바이트 문자 집합) 형식인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 값을 유니코드로 변환합니다.  
  
 지정된 언어가 잘못되었거나 해당 언어에 해당하는 리소스가 설치되지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오류를 반환합니다. 중립 언어 리소스를 사용하려면 0x0을 *language_term*으로 지정합니다.  
  
 \<*contains_search_condition*>  
 *column_name*에서 검색할 텍스트와 일치 조건을 지정합니다.  
  
*\<contains_search_condition>* 은 **nvarchar**입니다. 암시적 변환은 다른 문자 데이터 형식이 입력으로 사용될 때 발생합니다. 큰 문자열 데이터 형식 nvarchar (max) 및 varchar(max)를 사용할 수 없습니다. 다음 예에서는 `@SearchWord`로 정의된 `varchar(30)` 변수로 인해 `CONTAINS` 조건자에서 암시적 변환이 발생합니다.
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord VARCHAR(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 변환 시 "매개 변수 스니핑"이 작동하지 않으므로 성능 향상을 위해 **nvarchar**를 사용합니다. 이 예에서는 `@SearchWord`를 `nvarchar(30)`로 선언합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord NVARCHAR(30)  
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
단어나 구가 정확하게 일치하는 항목을 지정합니다. 유효한 단순 단어의 예로는 "blue berry", blueberry, "Microsoft SQL Server" 등이 있습니다. 구는 큰따옴표("")로 묶어야 합니다. 구에 포함된 단어는 *\<contains_search_condition>* 에 지정된 것과 같은 순서로 데이터베이스 열에 나타나야 합니다. 단어나 구에서 문자를 검색할 때는 대/소문자를 구분하지 않습니다. 전체 텍스트 인덱싱된 열에서 의미 없는 단어 또는 [중지 단어](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)(예: a, and, the)는 전체 텍스트 인덱스에 저장되지 않습니다. 단일 단어 검색에 의미 없는 단어가 사용되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 쿼리에 의미 없는 단어만 포함되어 있다는 오류 메시지를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 \Mssql\Binn\FTERef 디렉터리에 의미 없는 단어 표준 목록이 포함되어 있습니다.  
  
 문장 부호는 무시됩니다. 따라서 `CONTAINS(testing, "computer failure")`는 "Where is my computer? Failure to find it would be expensive."라는 값을 가진 행을 검색합니다. 단어 분리기 작동에 대한 자세한 내용은 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)를 참조하세요.  
  
 \<prefix_term>  
 지정한 텍스트로 시작하는 단어 또는 구를 검색하도록 지정합니다. 접두사 단어를 큰따옴표("")로 묶고 뒤에 있는 따옴표 앞에 별표(\*)를 추가하면 별표 앞에 지정된 단순 단어로 시작하는 모든 텍스트가 검색됩니다. 절은 `CONTAINS (column, '"text*"')`와 같이 지정해야 합니다. 별표는 단어나 구에 포함된 어근의 문자를 개수에 관계없이 검색합니다. 텍스트와 별표를 큰따옴표로 구분하지 않으면 조건자가 `CONTAINS (column, 'text*')`를 읽고 전체 텍스트 검색에서 별표를 문자로 간주하여 `text*`와 정확하게 일치하는 텍스트를 검색합니다. 일반적으로 단어 분리기는 별표(\*)와 같은 문자를 무시하므로 전체 텍스트 엔진은 별표가 포함된 단어를 검색하지 않습니다.  
  
 *\<prefix_term>* 이 구일 경우 구에 포함된 각 단어는 별도의 접두사로 간주됩니다. 따라서 접두사 단어 "local wine*"을 지정하는 쿼리는 "local winery", "locally wined and dined" 등의 텍스트가 포함된 모든 행을 검색합니다.  
  
 \<generation_term>  
 포함된 단순 단어에 검색할 원래 단어에서 변형된 단어가 포함된 경우 단어를 검색하도록 지정합니다.  
  
 INFLECTIONAL  
 지정된 단순 단어에 언어별 형태소 분석기를 사용하도록 지정합니다. 형태소 분석기 동작은 각 언어의 형태소 분석 규칙에 따라 정의됩니다. 중립 언어에는 관련된 형태소 분석기가 없습니다. 쿼리할 열의 열 언어는 원하는 형태소 분석기를 참조하는 데 사용됩니다. *language_term*을 지정하면 해당 언어에 대한 형태소 분석기가 사용됩니다.  
  
 *\<generation_term>* 내에서 지정된 *\<simple_term>* 은 명사와 동사 중 하나만 검색합니다.  
  
 THESAURUS  
 열의 전체 텍스트 언어 또는 쿼리에 지정된 언어에 해당되는 동의어 사전이 사용되도록 지정합니다. *\<simple_term>* 에서 가장 긴 패턴에 대해 동의어 사전에서 대응되는 항목을 찾고 원래 패턴을 확장하거나 대체하도록 추가 단어가 생성됩니다. *\<simple_term>* 의 전체 또는 일부에 일치하는 항목을 찾을 수 없으면 일치하지 않는 부분이 *simple_term*으로 처리됩니다. 전체 텍스트 검색 동의어 사전에 대한 자세한 내용은 [전체 텍스트 검색에 사용할 동의어 사전 파일 구성 및 관리](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)를 참조하세요.  
  
 \<generic_proximity_term>  
 검색 대상 문서에 있어야 하는 단어 또는 구를 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] \<custom_proximity_term>을 사용할 것을 권장합니다.  
  
 NEAR | ~  
 일치 항목이 반환되려면 NEAR 또는 ~ 연산자의 양쪽에 있는 단어나 구가 문서에 있어야 함을 나타냅니다. 두 개의 검색 단어를 지정해야 합니다. 지정한 검색 단어는 큰따옴표("*phrase*")로 구분되는 특정 단어나 구가 될 수 있습니다.  
  
 `a NEAR b NEAR c` 또는 `a ~ b ~ c`와 같이 근접 단어를 여러 개 연결할 수 있습니다. 일치 항목이 반환되려면 연결된 근접 단어가 모두 해당 문서에 있어야 합니다.  
  
 예를 들어 `CONTAINS(*column_name*, 'fox NEAR chicken')` 및 `CONTAINSTABLE(*table_name*, *column_name*, 'fox ~ chicken')`은 둘 다 지정된 열에서 "fox"와 "chicken"을 모두 포함하는 문서를 반환합니다. 또한 CONTAINSTABLE은 "fox" 및 "chicken"의 근접 정도에 따라 각 문서의 순위를 반환합니다. 예를 들어 문서에 "The fox ate the chicken"이라는 문장이 있으면 다른 문서에 비해 단어가 서로 가까이 있으므로 문서 순위가 높아집니다.  
  
 일반 근접 용어에 대한 자세한 내용은 [NEAR를 사용하여 근접 단어 검색](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)을 참조하세요.  
  
 \<custom_proximity_term>  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상
  
 일치시킬 단어나 구를 지정하고 선택적으로 검색 단어 사이에 허용할 최대 거리를 지정합니다. 검색 단어를 지정한 것과 동일한 순서로 찾도록 지정할 수도 있습니다(\<match_order>).  
  
 지정한 검색 단어는 큰따옴표("*phrase*")로 구분되는 특정 단어나 구가 될 수 있습니다. 일치 항목이 반환되려면 지정한 단어가 모두 해당 문서에 있어야 합니다. 두 단어 이상을 지정해야 합니다. 최대 검색 단어 수는 64입니다.  
  
 기본적으로 사용자 지정 근접 단어는 지정한 단어 사이의 거리 및 순서와 관계없이 해당 단어가 포함된 행을 모두 반환합니다. 예를 들어 다음 쿼리를 일치시키려면 문서에 `term1` 및 "`term3 term4`"이 순서와 위치에 관계없이 포함되어야 합니다.  
  
```sql  
CONTAINS(column_name, 'NEAR(term1,"term3 term4")')  
```  
  
 선택적 매개 변수는 다음과 같습니다.  
  
 \<maximum_distance>  
 문자열이 일치 항목으로 처리될 수 있는 순서로 문자열 처음과 끝에 검색 단어 사이에 허용되는 최대 거리를 지정합니다.  
  
 *integer*  
 0에서 4294967295 사이의 양의 정수를 지정합니다. 이 값은 지정한 추가 검색 단어를 제외한 처음과 마지막 검색 단어 사이에 올 수 있고 검색 대상이 아닌 단어 수를 제어합니다.  
  
 예를 들어 다음 쿼리는 어떤 순서로든 최대 거리 5 이내의 `AA` 및 `BB`를 검색합니다.  
  
```sql  
CONTAINS(column_name, 'NEAR((AA,BB),5)')  
```  
  
 `AA one two three four five BB` 문자열은 일치 항목입니다. 다음 예에서는 쿼리가 세 개의 검색 단어 `AA`, `BB` 및 `CC`에 대해 최대 거리 5 이내로 검색 단어를 지정합니다.  
  
```sql  
CONTAINS(column_name, 'NEAR((AA,BB,CC),5)')  
```  
  
 이 쿼리는 전체 거리가 5인 다음 문자열을 일치시킵니다.  
  
 `BB   one two   CC   three four five A  A`  
  
 내부 검색 단어 `CC`는 계산하지 않습니다.  
  
 **MAX**  
 지정된 단어 사이의 거리와 관계없이 해당 단어가 포함된 행을 모두 반환합니다. 이것이 기본값입니다.  
  
 \<match_order>  
 검색 쿼리에서 반환하도록 지정한 순서로 단어가 나올지 여부를 지정합니다. \<match_order>를 지정하려면 \<maximum_distance>도 지정해야 합니다.  
  
 \<match_order>는 다음 값 중 하나를 사용합니다.  
  
 **TRUE**  
 단어에 지정한 순서를 적용합니다. 예를 들어 `NEAR(A,B)`는 `A ... B`에만 일치합니다.  
  
 **FALSE**  
 지정한 순서를 무시합니다. 예를 들어 `NEAR(A,B)`는 `A ... B` 및 `B ... A`와 모두 일치합니다.  
  
 이것이 기본값입니다.  
  
 예를 들어 다음 근접 단어는 거리와 관계없이 지정한 순서로 "`Monday`", "`Tuesday`" 및 "`Wednesday`" 단어를 검색합니다.  
  
```sql  
CONTAINS(column_name, 'NEAR ((Monday, Tuesday, Wednesday), MAX, TRUE)')  
```  
  
 사용자 지정 근접 용어 사용에 대한 자세한 내용은 [NEAR를 사용하여 근접 단어 검색](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)을 참조하세요.  
  
 \<weighted_term>  
 쿼리에서 반환된 결과 행이 단어 및 구 목록과 일치하고 선택적으로 가중치 값이 지정되도록 합니다.  
  
 ISABOUT  
 *\<weighted_term>* 키워드를 지정합니다.  
  
 WEIGHT(*weight_value*)  
 0\.0에서 1.0 사이의 숫자로 가중치를 지정합니다. *\<weighted_term>* 의 각 구성 요소에 *weight_value*가 포함될 수 있습니다. *weight_value*를 사용하여 쿼리의 각 부분이 쿼리와 일치하는 각 행에 할당되는 등급 값에 영향을 주는 방법을 변경할 수 있습니다. WEIGHT는 CONTAINS 쿼리 결과에는 영향을 주지 않지만 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 쿼리의 순위에는 영향을 줍니다.  
  
> [!NOTE]  
> 소수 구분 기호는 운영 체제 로캘에 관계없이 항상 마침표입니다.  
  
 { AND \| & } \| { AND NOT \| &! } \| { OR \| \| }  
 두 개의 포함 검색 조건 간에 논리적 연산을 지정합니다.  
  
 { AND \| & }  
 두 개의 포함 검색 조건이 모두 충족되어야 일치한다는 것을 나타냅니다. AND 키워드 대신 앰퍼샌드 기호(&)를 사용하여 AND 연산자를 나타낼 수도 있습니다.  
  
 { AND NOT \| &! }  
 두 번째 검색 조건이 일치하지 않아야 한다는 것을 나타냅니다. AND NOT 키워드 대신 앰퍼샌드 다음에 느낌표 기호(&)를 사용하여 AND NOT 연산자를 나타낼 수도 있습니다.  
  
 { OR \| \| }  
 두 개의 포함 검색 조건 중 하나가 충족되어야 일치한다는 것을 나타냅니다. OR 키워드 대신 막대 기호(|)를 사용하여 OR 연산자를 나타낼 수도 있습니다.  
  
 *\<contains_search_condition>* 에 괄호로 묶은 그룹이 있으면 이러한 그룹이 가장 먼저 평가됩니다. 괄호로 묶인 그룹을 평가한 후 포함 검색 조건에 논리 연산자를 사용할 때 다음 규칙이 적용됩니다.  
  
-   AND보다 NOT이 먼저 적용됩니다.  
  
-   AND NOT과 같이 NOT은 AND 다음에만 올 수 있으며 OR NOT 연산자는 허용되지 않습니다. NOT은 첫 번째 단어 앞에 지정할 수 없습니다. 예를 들어 `CONTAINS (mycolumn, 'NOT "phrase_to_search_for" ' )`는 유효하지 않습니다.  
  
-   OR보다 AND가 먼저 적용됩니다.  
  
-   동일한 유형의 부울 연산자(AND, OR)는 결합성을 가지므로 어떤 순서로든 적용할 수 있습니다.  
  
 *n*  
 여러 CONTAINS 검색 조건과 용어를 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 전체 텍스트 조건자와 함수는 단일 테이블에서 작동합니다. 이 사실은 FROM 조건자에 표시됩니다. 여러 테이블을 검색하려면 FROM 절에 조인된 테이블을 사용하여 두 개 이상의 테이블을 합한 결과 집합을 대상으로 검색 작업을 수행합니다.  
  
 데이터베이스 호환성 수준이 100으로 설정된 경우에는 [OUTPUT 절](../../t-sql/queries/output-clause-transact-sql.md) 에 전체 텍스트 조건자가 허용되지 않습니다.  
  
## <a name="querying-remote-servers"></a>원격 서버 쿼리  
 CONTAINS 또는 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 조건자에 네 부분으로 된 이름을 사용하여 연결된 서버의 대상 테이블에 대한 전체 텍스트 인덱싱된 열을 쿼리할 수 있습니다. 원격 서버에서 전체 텍스트 쿼리를 받도록 준비하려면 원격 서버의 대상 테이블 및 열에 대한 전체 텍스트 인덱스를 만든 다음 원격 서버를 연결된 서버로 추가합니다.  
  
## <a name="comparison-of-like-to-full-text-search"></a>LIKE와 전체 텍스트 검색 비교  
 전체 텍스트 검색과 달리 [LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 조건자는 문자 패턴에 대해서만 적용됩니다. 또한 LIKE 조건자는 서식 있는 이진 데이터를 쿼리하는 데 사용할 수도 없습니다. 특히 구조화되지 않은 많은 텍스트 데이터에 대한 LIKE 쿼리는 동일한 데이터에 대한 전체 텍스트 쿼리보다 훨씬 느립니다. 수백만 개의 텍스트 데이터 행에 대한 LIKE 쿼리는 결과가 반환되기까지 몇 분이 걸릴 수 있지만 동일한 데이터에 대한 전체 텍스트 쿼리는 반환되는 행 수와 해당 크기에 따라 몇 초 내에 완료됩니다. LIKE는 전체 테이블의 단순 패턴 스캔만 수행한다는 점도 고려하십시오. 반대로 전체 텍스트 쿼리는 언어를 인식하며 인덱스 및 쿼리 시 중지 단어 필터링, 동의어 사전 및 활용 형태상의 확장과 같은 특정 변환을 적용합니다. 이러한 변환을 통해 전체 텍스트 쿼리의 재호출 및 최종 결과 순위가 향상됩니다.  
  
## <a name="querying-multiple-columns-full-text-search"></a>여러 열 쿼리(전체 텍스트 검색)  
 검색할 열 목록을 지정하여 여러 열을 쿼리할 수 있습니다. 열은 동일한 테이블에 있어야 합니다.  
  
 예를 들어 다음 CONTAINS 쿼리는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스 `Production.Product` 테이블의 `Name` 및 `Color` 열에서 `Red`라는 단어를 검색합니다.  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Name, Color   
FROM Production.Product  
WHERE CONTAINS((Name, Color), 'Red');  
```  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-contains-with-simple_term"></a>A. CONTAINS를 \<simple_term>과 함께 사용  
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
  
### <a name="b-using-contains-and-phrase-with-simple_term"></a>B. CONTAINS 및 구를 \<simple_term>과 함께 사용  
 다음 예에서는 `Mountain`이나 `Road`라는 구가 포함된 모든 제품을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' Mountain OR Road ')  
GO  
```  
  
### <a name="c-using-contains-with-prefix_term"></a>C. CONTAINS를 \<prefix_term>과 함께 사용  
 다음 예에서는 `Name` 열에 접두사 chain으로 시작하는 단어가 하나 이상인 모든 제품 이름을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' "Chain*" ');  
GO  
```  
  
### <a name="d-using-contains-and-or-with-prefix_term"></a>D. CONTAINS 및 OR을 \<prefix_term>과 함께 사용  
 다음 예에서는 접두사가 `chain` 또는 `full`인 문자열을 포함하는 모든 범주 설명을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, '"chain*" OR "full*"');  
GO  
```  
  
### <a name="e-using-contains-with-proximity_term"></a>E. CONTAINS를 \<proximity_term>과 함께 사용  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 
  
 다음 예에서는 `Production.ProductReview` 테이블에서 단어 "`bike`"의 10 단어 이내로 지정한 순서에 따라 "`control`" 단어가 포함된 모든 설명을 검색합니다. 즉, "`bike`"는 "`control`"보다 우선합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments , 'NEAR((bike,control), 10, TRUE)');  
GO  
```  
  
### <a name="f-using-contains-with-generation_term"></a>F. CONTAINS를 \<generation_term>과 함께 사용  
 다음 예에서는 riding, ridden 등 `ride`에서 파생된 단어가 있는 모든 제품을 검색합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, ' FORMSOF (INFLECTIONAL, ride) ');  
GO  
```  
  
### <a name="g-using-contains-with-weighted_term"></a>G. CONTAINS를 \<weighted_term>과 함께 사용  
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
  
### <a name="h-using-contains-with-variables"></a>H. 변수에 CONTAINS 사용  
 다음 예에서는 특정 검색 용어 대신 변수를 사용합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord NVARCHAR(30)  
SET @SearchWord = N'Performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
GO  
```  
  
### <a name="i-using-contains-with-a-logical-operator-and"></a>9\. 논리 연산자(AND)에 CONTAINS 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 ProductDescription 테이블을 사용합니다. 이 쿼리에서는 CONTAINS 조건자를 사용하여 설명 ID가 5가 아니고 `Aluminum`과 `spindle`이라는 단어가 둘 다 포함된 설명을 검색합니다. 검색 조건에는 AND 부울 연산자가 사용됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'Aluminum AND spindle');  
GO  
```  
  
### <a name="j-using-contains-to-verify-a-row-insertion"></a>J. CONTAINS를 사용하여 행 삽입 확인  
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
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 
  
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
  
## <a name="see-also"></a>참고 항목  
 [전체 텍스트 검색 시작](../../relational-databases/search/get-started-with-full-text-search.md)   
 [전체 텍스트 카탈로그 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [전체 텍스트 검색 쿼리 만들기&#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
