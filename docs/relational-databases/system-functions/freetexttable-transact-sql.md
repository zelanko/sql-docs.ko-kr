---
title: FREETEXTTABLE (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FREETEXTTABLE_TSQL
- FREETEXTTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- search conditions [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXTTABLE function (Transact-SQL)
- ranked results [full-text search]
- column searches [full-text search]
ms.assetid: 4523ae15-4260-40a7-a53c-8df15e1fee79
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ab1797fabd8fb7d77eab85c97604b77e72f25c3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68042766"
---
# <a name="freetexttable-transact-sql"></a>FREETEXTTABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  문자 기반 데이터 형식이 포함 된 전체 텍스트 인덱싱된 열 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색을 수행 하기 위해 SELECT 문의 [FROM 절](../../t-sql/queries/from-transact-sql.md) 에 사용 되는 함수입니다. 이 함수는 지정 된 *freetext_string*에 있는 텍스트의 의미와 일치 하는 값을 포함 하는 값을 포함 하는 열에 대해 0 개 이상의 행이 포함 된 테이블을 반환 합니다. FREETEXTTABLE은 일반 테이블 이름처럼 참조됩니다.  
  
 FREETEXTTABLE는 [FREETEXT &#40;transact-sql&#41;](../../t-sql/queries/freetext-transact-sql.md)와 동일한 종류의 일치에 유용 합니다.  
  
 FREETEXTTABLE을 사용하는 쿼리는 각 행에 대해 적절한 순위 값(RANK) 및 전체 텍스트 키(KEY)를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 전체 텍스트 검색 형식에 대한 자세한 내용은 [전체 텍스트 검색이 있는 쿼리](../../relational-databases/search/query-with-full-text-search.md)를 참조하세요.  
  
(https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
FREETEXTTABLE (table , { column_name | (column_list) | * }   
          , 'freetext_string'   
     [ , LANGUAGE language_term ]   
     [ , top_n_by_rank ] )  
```  
  
## <a name="arguments"></a>인수  
 *table*  
 전체 텍스트 쿼리용으로 표시된 테이블 이름입니다. *테이블이* 나 *뷰*는 한 부분, 두 부분 또는 세 부분으로 구성 된 데이터베이스 개체 이름일 수 있습니다. 뷰를 쿼리할 때는 전체 텍스트 인덱싱된 기본 테이블 하나만 포함할 수 있습니다.  
  
 *테이블이* 서버 이름을 지정할 수 없으며 연결 된 서버에 대 한 쿼리에서 사용할 수 없습니다.  
  
 *column_name*  
 FROM 절에 지정된 테이블에 대한 하나 이상의 전체 텍스트 인덱싱된 열의 이름입니다. 열은 **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** 또는 **varbinary(max)** 형식이 될 수 있습니다.  
  
 *column_list*  
 여러 개의 열을 쉼표로 구분하여 지정할 수 있음을 나타냅니다. *column_list*는 괄호로 묶어야 합니다. *language_term*을 지정하지 않을 경우 *column_list*에 있는 모든 열의 언어가 같아야 합니다.  
  
 \*  
 주어진 *freetext_string*을 검색하는 데 전체 텍스트 검색용으로 등록된 모든 열을 사용하도록 지정합니다. *Language_term* 지정 하지 않으면 테이블의 모든 전체 텍스트 인덱싱된 열 언어가 동일 해야 합니다.  
  
 *freetext_string*  
 *column_name*에서 검색할 텍스트입니다. 단어, 구 또는 문장을 포함하여 모든 텍스트를 입력할 수 있습니다. 모든 용어나 용어의 형식이 전체 텍스트 인덱스에 있으면 일치하는 항목이 생성됩니다.  
  
 AND가 키워드인 CONTAINS 검색 조건과 달리 *freetext_string* 에서 사용 하는 경우 ' a l s '는 의미 없는 단어 또는 [중지 단어](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)로 간주 되어 무시 됩니다.  
  
 WEIGHT, FORMSOF, 와일드카드, NEAR 및 기타 구문은 사용할 수 없습니다. *freetext_string*은 단어가 분리되고 형태소가 분석되며 동의어 사전을 통해 전달됩니다.  
  
 LANGUAGE *language_term*  
 쿼리의 일부로 단어 분리, 형태소 분석, 동의어 사전 및 중지 단어 제거에 리소스를 사용할 언어입니다. 이 매개 변수는 선택적이며 언어의 LCID(로캘 ID)에 해당하는 문자열, 정수 또는 16진수 값으로 지정할 수 있습니다. *language_term*을 지정할 경우 해당 언어는 검색 조건의 모든 요소에 적용됩니다. 값을 지정하지 않으면 열의 전체 텍스트 언어가 사용됩니다.  
  
 언어가 다른 문서가 단일 열에 BLOB(Binary Large Object)으로 함께 저장된 경우 지정된 문서의 LCID(로캘 ID)에 따라 해당 내용을 인덱싱하는 데 사용할 언어가 결정됩니다. 이러한 열을 쿼리할 때 *LANGUAGE language_term* 지정 하면 일치 하는 항목의 확률을 높일 수 있습니다.  
  
 문자열로 지정하는 경우 *language_term*은 [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 호환성 뷰의 **alias** 열 값에 해당합니다.  문자열은 '*language_term*'과 같이 작은따옴표로 묶어야 합니다. 정수로 지정하는 경우 *language_term*은 언어를 식별하는 실제 LCID입니다. 16진수 값으로 지정하는 경우 *language_term*은 0x로 시작하는 16진수 LCID 값입니다. 16진수 값은 앞에 오는 0을 포함하여 8자리 수를 초과할 수 없습니다.  
  
 값이 DBCS (더블 바이트 문자 집합) 형식인 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우는이를 유니코드로 변환 합니다.  
  
 지정된 언어가 잘못되었거나 해당 언어에 해당하는 리소스가 설치되지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오류를 반환합니다. 중립 언어 리소스를 사용하려면 0x0을 *language_term*으로 지정합니다.  
  
 *top_n_by_rank*  
 내림차순으로 가장 높은 *n*개의 일치 하는 항목만 반환 되도록 지정 합니다. 정수 값 *n*이 지정 된 경우에만 적용 됩니다. *top_n_by_rank* 를 다른 매개 변수와 함께 사용하면 실제로 모든 조건자와 일치하는 행 수보다 적은 수의 행이 반환될 수 있습니다. *top_n_by_rank* 를 사용 하면 관련성이 가장 높은 항목만 회수 하 여 쿼리 성능을 높일 수 있습니다.  
  
## <a name="remarks"></a>설명  
 전체 텍스트 조건자와 함수는 단일 테이블에서 작동합니다. 이 사실은 FROM 조건자에 표시됩니다. 여러 테이블을 검색하려면 FROM 절에 조인된 테이블을 사용하여 두 개 이상의 테이블을 합한 결과 집합을 대상으로 검색 작업을 수행합니다.  
  
 FREETEXTTABLE은 FREETEXT 조건자와 동일한 검색 조건을 사용합니다.  
  
 CONTAINSTABLE와 마찬가지로 반환 된 테이블에는 **키** 및 **순위**라는 열이 있습니다 .이 열에는 적절 한 행을 가져오고 행 순위 값을 사용 하기 위해 쿼리 내에서 참조 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 FREETEXTTABLE은 지정된 테이블이나 테이블에서 참조되는 열에 대해 적절한 SELECT 권한이 있는 사용자만 호출할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example"></a>A. 간단한 예  
 다음 예에서는 3 개의 군을 나열 하 고 플래그에 색을 나열 하는 두 개의 열로 이루어진 간단한 테이블을 만들고 채웁니다. 이 예제에서는 테이블에 대 한 전체 텍스트 카탈로그 및 인덱스를 만들고 채웁니다. 그런 다음 **FREETEXTTABLE** 구문을 보여 줍니다.  
  
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
  
### <a name="b-using-freetext-in-an-inner-join"></a>B. INNER JOIN에 FREETEXT 사용  
 다음 예에서는의 `high level of performance`의미와 일치 하는 설명이 포함 된 제품의 설명 및 순위를 반환 합니다.  
  
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
  
### <a name="c-specifying-language-and-highest-ranked-matches"></a>C. 언어 및 최고 등급 일치 항목 지정  
 다음 예제는 동일 하며 `LANGUAGE` *language_term* 및 *top_n_by_rank* 매개 변수를 사용 하는 방법을 보여 줍니다.  
  
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
>  LANGUAGE *language_term* 매개 변수는 *top_n_by_rank* 매개 변수를 사용 하는 데 필요 하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [전체 텍스트 검색 시작](../../relational-databases/search/get-started-with-full-text-search.md)   
 [전체 텍스트 카탈로그 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)   
 [전체 텍스트 검색 쿼리 만들기&#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [&#40;Transact-sql&#41;를 포함 합니다.](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [행 집합 함수 &#40;Transact-sql&#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [precompute rank 서버 구성 옵션](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md)  
  
  
