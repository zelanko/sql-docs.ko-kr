---
title: FREETEXTTABLE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREETEXTTABLE_TSQL
- FREETEXTTABLE
dev_langs: TSQL
helpviewer_keywords:
- search conditions [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXTTABLE function (Transact-SQL)
- ranked results [full-text search]
- column searches [full-text search]
ms.assetid: 4523ae15-4260-40a7-a53c-8df15e1fee79
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 32d2f6ab0ec5faf5603504824ec6917f0297ef72
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="freetexttable-transact-sql"></a>FREETEXTTABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  사용 되는 함수는 [FROM 절](../../t-sql/queries/from-transact-sql.md) 의 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 문을 수행 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색 전체 텍스트 인덱싱된 열의 문자 기반 데이터 형식이 포함 된 합니다. 이 함수는 0, 1 또는 의미와 뿐 아니라 정확한 단어는 지정 된 텍스트의 일치 하는 값이 포함 된 열에 대 한 더 많은 행의 테이블을 반환 *freetext_string*합니다. FREETEXTTABLE은 일반 테이블 이름처럼 참조됩니다.  
  
 FREETEXTTABLE은 동일한 종류의 일치 하는 데 유용는 [FREETEXT &#40; Transact SQL &#41; ](../../t-sql/queries/freetext-transact-sql.md),  
  
 FREETEXTTABLE을 사용하는 쿼리는 각 행에 대해 적절한 순위 값(RANK) 및 전체 텍스트 키(KEY)를 반환합니다.  
  
> [!NOTE]  
>  전체 텍스트 검색에서 지원 되는 형식에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 참조 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)합니다.  
  
(http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)). |  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
FREETEXTTABLE (table , { column_name | (column_list) | * }   
          , 'freetext_string'   
     [ , LANGUAGE language_term ]   
     [ , top_n_by_rank ] )  
```  
  
## <a name="arguments"></a>인수  
 *table*  
 전체 텍스트 쿼리용으로 표시된 테이블 이름입니다. *테이블* 또는 *보기*1 개, 2 개 또는 세 부분으로 구성 된 데이터베이스 개체 이름일 수 있습니다. 뷰를 쿼리할 때는 전체 텍스트 인덱싱된 기본 테이블 하나만 포함할 수 있습니다.  
  
 *테이블* 서버 이름을 지정할 수 없습니다 및 연결 된 서버에 대 한 쿼리에서 사용할 수 없습니다.  
  
 *column_name*  
 FROM 절에 지정된 테이블에 대한 하나 이상의 전체 텍스트 인덱싱된 열의 이름입니다. 열 형식이 될 수 있습니다 **char**, **varchar**, **nchar**, **nvarchar**, **텍스트**, **ntext**, **이미지**, **xml**, **varbinary**, 또는 **varbinary (max)**합니다.  
  
 *column_list*  
 여러 개의 열을 쉼표로 구분하여 지정할 수 있음을 나타냅니다. *column_list* 괄호로 묶어야 합니다. 하지 않는 한 *language_term* 지정 된 언어의 모든 열 *column_list* 동일 해야 합니다.  
  
 \*  
 전체 텍스트 검색을 위해 등록 된 모든 열에 대 한 검색을 사용 해야 함을 지정는 주어진 *freetext_string*합니다. 하지 않는 한 *language_term* 지정, 테이블의 모든 전체 텍스트 인덱싱된 열의 언어가 동일 해야 합니다.  
  
 *freetext_string*  
 검색할 텍스트는 *column_name*합니다. 단어, 구 또는 문장을 포함하여 모든 텍스트를 입력할 수 있습니다. 모든 용어나 용어의 형식이 전체 텍스트 인덱스에 있으면 일치하는 항목이 생성됩니다.  
  
 와 달리 CONTAINS 검색 조건과 AND가 키워드인을 사용할 경우 *freetext_string* 단어 '및' 의미 없는 단어 것으로 간주 됩니다 또는 [중지 단어](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md), 무시 됩니다.  
  
 WEIGHT, FORMSOF, 와일드카드, NEAR 및 기타 구문은 사용할 수 없습니다. *freetext_string* 단어가 형태소가 분석 되며 동의어 사전을 통해 전달 합니다.  
  
 언어 *language_term*  
 쿼리의 일부로 단어 분리, 형태소 분석, 동의어 사전 및 중지 단어 제거에 리소스를 사용할 언어입니다. 이 매개 변수는 선택적이며 언어의 LCID(로캘 ID)에 해당하는 문자열, 정수 또는 16진수 값으로 지정할 수 있습니다. 경우 *language_term* , 지정한 언어는 검색 조건의 모든 요소에 적용 됩니다. 값을 지정하지 않으면 열의 전체 텍스트 언어가 사용됩니다.  
  
 언어가 다른 문서가 단일 열에 BLOB(Binary Large Object)으로 함께 저장된 경우 지정된 문서의 LCID(로캘 ID)에 따라 해당 내용을 인덱싱하는 데 사용할 언어가 결정됩니다. 이러한 열을 쿼리할 때 지정 *언어**language_term* 가장 잘 맞는의 확률을 높일 수 있습니다.  
  
 문자열로 지정 하는 경우 *language_term* 에 해당 하는 **별칭** 열 값에는 [sys.syslanguages&#40; Transact SQL &#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 호환성 보기.  와 같이 하나의 따옴표로 묶어야 합니다 문자열 '*language_term*'. 정수로 지정 된 경우 *language_term* 는 언어를 식별 하는 실제 LCID입니다. 16 진수 값으로 지정 하는 경우 *language_term* 된 LCID의 16 진수 값은 0x 시작 합니다. 16진수 값은 선행 0을 포함하여 8자리 수를 초과할 수 없습니다.  
  
 더블 바이트 문자 집합 (DBCS) 형식인 경우에 값이 있으면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 유니코드로 변환 됩니다.  
  
 지정된 언어가 잘못되었거나 해당 언어에 해당하는 리소스가 설치되지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오류를 반환합니다. 중립 언어 리소스를 사용 하려면 0x0 지정 *language_term*합니다.  
  
 *top_n_by_rank*  
 만 지정 된  *n* 내림차순으로 최고 등급된 일치 항목 반환 됩니다. 정수 값을 경우에 적용 됩니다.  *n* 를 지정 합니다. *top_n_by_rank* 를 다른 매개 변수와 함께 사용하면 실제로 모든 조건자와 일치하는 행 수보다 적은 수의 행이 반환될 수 있습니다. *top_n_by_rank* 가장 관련성이 높은 항목만 회수 하 여 쿼리 성능을 높일 수 있습니다.  
  
## <a name="remarks"></a>주의  
 전체 텍스트 조건자와 함수는 단일 테이블에서 작동합니다. 이 사실은 FROM 조건자에 표시됩니다. 여러 테이블을 검색하려면 FROM 절에 조인된 테이블을 사용하여 두 개 이상의 테이블을 합한 결과 집합을 대상으로 검색 작업을 수행합니다.  
  
 FREETEXTTABLE은 FREETEXT 조건자와 동일한 검색 조건을 사용합니다.  
  
 CONTAINSTABLE 처럼 반환 되는 테이블에 명명 된 열 **키** 및 **순위**, 쿼리를 적절 한 행을 가져오고 행 순위 값을 사용 하 여 내에서 참조 되는 합니다.  
  
## <a name="permissions"></a>Permissions  
 FREETEXTTABLE은 지정된 테이블이나 테이블에서 참조되는 열에 대해 적절한 SELECT 권한이 있는 사용자만 호출할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example"></a>1. 간단한 예  
 다음 예제에서는 만들고 두 열로 3 군 및 해당 플래그와의 색을 나열 하는 간단한 테이블을 채웁니다. It가 만들고 전체 텍스트 카탈로그 및 테이블에 인덱스를 채웁니다. 그런 다음 **FREETEXTTABLE** 구문을 보여 줍니다.  
  
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
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Blue');  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Yellow');  
```  
  
### <a name="b-using-freetext-in-an-inner-join"></a>2. INNER JOIN에 FREETEXT 사용  
 다음 예에서는 `sweet`, `candy`, `bread`, `dry` 또는 `meat`와 연관된 모든 범주에 대해 범주 이름과 설명을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance') AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
### <a name="c-specifying-language-and-highest-ranked-matches"></a>3. 언어 및 최고 등급 일치 항목 지정  
 다음 예제는 동일 하 고 사용 하 여는 `LANGUAGE` *language_term* 및 *top_n_by_rank* 매개 변수입니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance',  
    LANGUAGE N'English', 2) AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
> [!NOTE]  
>  언어 *language_term* paramete*r* 사용할 필요가 없습니다는 *top_n_by_rank* 매개 변수*합니다.*  
  
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
 [FREETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [행 집합 함수 &#40; Transact SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [순위 사전 계산 서버 구성 옵션](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md)  
  
  
