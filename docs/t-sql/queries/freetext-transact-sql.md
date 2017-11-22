---
title: FREETEXT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREETEXT
- FREETEXT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXT predicate (Transact-SQL)
- words in predicate [full-text search]
- column searches [full-text search]
ms.assetid: 2f199d3c-440e-4bcf-bdb5-82bb3994005d
caps.latest.revision: "44"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9c7475e73cbd5022bf5c243fbd4e7a35dc115cf0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="freetext-transact-sql"></a>FREETEXT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용 되는 조건자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] [WHERE 절](../../t-sql/queries/where-transact-sql.md) 의 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 문을 수행 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색 전체 텍스트 인덱싱된 열의 문자 기반 데이터 형식이 포함 된 합니다. 이 조건자는 검색 조건의 의미와 일치하지만 단어가 정확히 일치하지 않는 값을 검색합니다. FREETEXT를 사용 하는 경우 전체 텍스트 쿼리 엔진이 내부적으로 다음 작업이 수행 된 *freetext_string*각 용어에 가중치를 할당 한 다음 일치 항목을 찾습니다.  
  
-   단어 경계를 기반으로 문자열을 개별 단어로 구분합니다(단어 분리).  
  
-   단어의 활용 형태를 생성합니다(형태소 분석).  
  
-   동의어 사전에서 찾은 일치 항목을 기반으로 용어에 대한 확장 또는 대체 목록을 식별합니다.  
  
> [!NOTE]  
>  전체 텍스트 검색에서 지원 되는 형식에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 참조 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
FREETEXT ( { column_name | (column_list) | * }   
          , 'freetext_string' [ , LANGUAGE language_term ] )  
```  
  
## <a name="arguments"></a>인수  
 *column_name*  
 FROM 절에 지정된 테이블에 대한 하나 이상의 전체 텍스트 인덱싱된 열의 이름입니다. 열 형식이 될 수 있습니다 **char**, **varchar**, **nchar**, **nvarchar**, **텍스트**, **ntext**, **이미지**, **xml**, **varbinary**, 또는 **varbinary (max)**합니다.  
  
 *column_list*  
 여러 개의 열을 쉼표로 구분하여 지정할 수 있음을 나타냅니다. *column_list* 괄호로 묶어야 합니다. 하지 않는 한 *language_term* 지정 된 언어의 모든 열 *column_list* 동일 해야 합니다.  
  
 \*  
 전체 텍스트 검색을 위해 등록 된 모든 열에 대 한 검색을 사용 해야 함을 지정는 주어진 *freetext_string*합니다. FROM 절에 둘 이상의 테이블 있으면 \* 테이블 이름으로 한정 되어야 합니다. 하지 않는 한 *language_term* 지정, 테이블의 모든 열의 언어가 동일 해야 합니다.  
  
 *freetext_string*  
 검색할 텍스트는 *column_name*합니다. 단어, 구 또는 문장을 포함하여 모든 텍스트를 입력할 수 있습니다. 모든 용어나 용어의 형식이 전체 텍스트 인덱스에 있으면 일치하는 항목이 생성됩니다.  
  
 와 달리 검색에 CONTAINS 및 CONTAINSTABLE에서 조건과 AND가 키워드인을 사용할 경우 *freetext_string* 단어 '및' 의미 없는 단어 것으로 간주 됩니다 또는 [중지 단어](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md), 무시 됩니다.  
  
 WEIGHT, FORMSOF, 와일드카드, NEAR 및 기타 구문은 사용할 수 없습니다. *freetext_string* 단어가 형태소가 분석 되며 동의어 사전을 통해 전달 합니다.  
  
 *freetext_string* 은 **nvarchar**합니다. 암시적 변환은 다른 문자 데이터 형식이 입력으로 사용될 때 발생합니다. 큰 문자열 데이터 형식 nvarchar (max) 및 varchar (max)를 사용할 수 없습니다. 다음 예에서는 `@SearchWord`로 정의된 `varchar(30)` 변수로 인해 `FREETEXT` 조건자에서 암시적 변환이 발생합니다.  
  
```  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 "매개 변수 스니핑" 변환에서 작동 하지 않고, 사용 하 여 **nvarchar** 성능 향상을 위해 합니다. 예제에서는 선언 `@SearchWord` 으로 `nvarchar(30)`합니다.  
  
```  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 최적화되지 않은 계획이 생성되는 경우 OPTIMIZE FOR 쿼리 힌트를 사용할 수도 있습니다.  
  
 언어 *language_term*  
 쿼리의 일부로 단어 분리, 형태소 분석, 동의어 사전 및 중지 단어 제거에 리소스를 사용할 언어입니다. 이 매개 변수는 선택적이며 언어의 LCID(로캘 ID)에 해당하는 문자열, 정수 또는 16진수 값으로 지정할 수 있습니다. 경우 *language_term* , 지정한 언어는 검색 조건의 모든 요소에 적용 됩니다. 값을 지정하지 않으면 열의 전체 텍스트 언어가 사용됩니다.  
  
 언어가 다른 문서가 단일 열에 BLOB(Binary Large Object)으로 함께 저장된 경우 지정된 문서의 LCID(로캘 ID)에 따라 해당 내용을 인덱싱하는 데 사용할 언어가 결정됩니다. 이러한 열을 쿼리할 때 지정 *언어**language_term* 가장 잘 맞는의 확률을 높일 수 있습니다.  
  
 문자열로 지정 하는 경우 *language_term* 에 해당 하는 **별칭** 열 값에 [sys.syslanguages&#40; Transact SQL &#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 호환성 보기.  와 같이 하나의 따옴표로 묶어야 합니다 문자열 '*language_term*'. 정수로 지정 된 경우 *language_term* 는 언어를 식별 하는 실제 LCID입니다. 16 진수 값으로 지정 하는 경우 *language_term* 된 LCID의 16 진수 값은 0x 시작 합니다. 16진수 값은 선행 0을 포함하여 8자리 수를 초과할 수 없습니다.  
  
 더블 바이트 문자 집합 (DBCS) 형식인 경우에 값이 있으면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 유니코드로 변환 됩니다.  
  
 지정 된 언어가 잘못 되었거나 없는 경우 리소스가 설치 되지 않은 해당 언어에 해당 하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 오류를 반환 합니다. 중립 언어 리소스를 사용 하려면 0x0 지정 *language_term*합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 전체 텍스트 조건자와 함수는 단일 테이블에서 작동합니다. 이 사실은 FROM 조건자에 표시됩니다. 여러 테이블을 검색하려면 FROM 절에 조인된 테이블을 사용하여 두 개 이상의 테이블을 합한 결과 집합을 대상으로 검색 작업을 수행합니다.  
  
FREETEXT를 사용하는 전체 텍스트 쿼리는 CONTAINS를 사용하는 전체 텍스트 쿼리보다 덜 정확합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색 엔진은 중요한 단어와 구를 식별합니다. 특별 한 의미는 예약 된 키워드 또는 와일드 카드 문자는 일반적으로 의미에서 지정 된 경우에 제공 되는 \<contains_search_condition > CONTAINS 조건자의 매개 변수입니다.
  
 전체 텍스트 조건자에서 허용 되지 않습니다는 [OUTPUT 절](../../t-sql/queries/output-clause-transact-sql.md) 데이터베이스 호환성 수준이 100으로 설정 된 경우.  
  
> [!NOTE]  
>  FREETEXTTABLE 함수는 FREETEXT 조건자와 같은 종류의 일치에 유용합니다. 이 함수에서 일반 테이블 이름 처럼 참조할 수는 [FROM 절](../../t-sql/queries/from-transact-sql.md) SELECT 문의 합니다. 자세한 내용은 참조 [FREETEXTTABLE &#40; Transact SQL &#41; ](../../relational-databases/system-functions/freetexttable-transact-sql.md).  
  
## <a name="querying-remote-servers"></a>원격 서버 쿼리  
 에 네 부분으로 된 이름을 사용할 수 있습니다는 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 또는 FREETEXT 조건자 전체 텍스트 쿼리 인덱싱된 연결 된 서버의 대상 테이블의 열입니다. 원격 서버에서 전체 텍스트 쿼리를 받도록 준비하려면 원격 서버의 대상 테이블 및 열에 대한 전체 텍스트 인덱스를 만든 다음 원격 서버를 연결된 서버로 추가합니다.  
  
## <a name="comparison-of-like-to-full-text-search"></a>LIKE와 전체 텍스트 검색 비교  
 전체 텍스트 검색과 달리 [LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 조건자는 문자 패턴에 대해서만 적용됩니다. 또한 LIKE 조건자는 서식 있는 이진 데이터를 쿼리하는 데 사용할 수도 없습니다. 특히 구조화되지 않은 많은 텍스트 데이터에 대한 LIKE 쿼리는 동일한 데이터에 대한 전체 텍스트 쿼리보다 훨씬 느립니다. 수백만 개의 텍스트 데이터 행에 대해 LIKE 쿼리를 실행하면 결과가 반환되기까지 몇 분이 걸릴 수 있지만 같은 데이터에 대해 전체 텍스트 쿼리를 실행하면 반환되는 행 수에 따라 몇 초 내에 완료됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-freetext-to-search-for-words-containing-specified-character-values"></a>1. FREETEXT를 사용하여 지정된 문자 값을 포함하는 단어 검색  
 다음 예에서는 vital, safety, components와 관련된 단어를 포함하는 문서를 모두 검색합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components' );  
GO  
```  
  
### <a name="b-using-freetext-with-variables"></a>2. FREETEXT에 변수 사용  
 다음 예에서는 특정 검색 용어 대신 변수를 사용합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30);  
SET @SearchWord = N'high-performance';  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [전체 텍스트 검색 시작](../../relational-databases/search/get-started-with-full-text-search.md)   
 [전체 텍스트 카탈로그 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [전체 텍스트 카탈로그 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [전체 텍스트 검색 쿼리 만들기&#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS&#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
