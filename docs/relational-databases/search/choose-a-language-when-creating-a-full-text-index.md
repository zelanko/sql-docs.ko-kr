---
description: 전체 텍스트 인덱스 생성 시 언어 선택
title: 전체 텍스트 인덱스 생성 시 언어 선택 | Microsoft 문서
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- full-text indexes [SQL Server], languages
- international considerations [full-text search]
- stemmers [full-text search]
- global considerations [full-text search]
- full-text search [SQL Server], international considerations
- languages [SQL Server], full-text indexes
- word breakers [full-text search]
ms.assetid: 670a5181-ab80-436a-be96-d9498fbe2c09
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f8c0860bb5ef874a6095b993478fa9cbc117fc4
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127769"
---
# <a name="choose-a-language-when-creating-a-full-text-index"></a>전체 텍스트 인덱스 생성 시 언어 선택

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  전체 텍스트 인덱스를 만들 때는 인덱싱된 열에 대한 열 수준 언어를 지정해야 합니다. 지정된 언어의 [단어 분리기 및 형태소 분석기](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) 는 인덱싱된 열에 대한 전체 텍스트 쿼리에 사용됩니다. 전체 텍스트 인덱스를 만들기 위해 열 언어를 선택할 때 고려할 몇 가지 사항이 있습니다. 이러한 고려 사항은 전체 텍스트 엔진으로 텍스트를 토큰화한 다음 인덱싱하는 방법과 관련이 있습니다.  
  
> [!NOTE]  
>  전체 텍스트 인덱스 열에 대한 열 수준 언어를 지정하려면 열을 지정할 때 LANGUAGE *language_term* 절을 사용합니다. 자세한 내용은 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md) 및 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)를 참조하세요.  
  
##  <a name="language-support-in-full-text-search"></a><a name="langsupp"></a> 전체 텍스트 검색의 언어 지원  
 이 섹션에서는 단어 분리기 및 형태소 분석기를 소개하고 전체 텍스트 검색에서 열 수준 언어의 LCID를 사용하는 방식에 대해 설명합니다.  
  
### <a name="introduction-to-word-breakers-and-stemmers"></a>단어 분리기 및 형태소 분석기 소개  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 이전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용되던 것보다 크게 향상된 완전히 새로운 단어 분리기 및 형태소 분석기 패밀리를 제공합니다.  
  
> [!NOTE]  
>  이러한 새로운 언어 구성 요소는 MS NLG(Microsoft Natural Language Group)에서 구현하고 지원합니다.  
  
 새로운 단어 분리기가 제공하는 이점은 다음과 같습니다.  
  
-   견고성  
  
     테스트 결과 새로운 단어 분리기는 쿼리 처리량이 많은 환경에서 강력한 성능을 제공하는 것으로 나타났습니다.  
  
-   보안  
  
     새로운 단어 처리기는 언어 구성 요소의 향상된 보안 기능 덕분에 SQL Server에서 기본적으로 사용하도록 설정되어 있습니다. SQL Server의 전반적인 보안 및 견고성을 향상시키려면 단어 분리기 및 필터와 같은 외부 구성 요소의 서명을 확인하는 것이 좋습니다. 이러한 구성 요소에 서명이 있는지 확인하도록 전체 텍스트를 구성하는 방법은 다음과 같습니다.  
  
    ```  
    EXEC sp_fulltext_service 'verify_signature';  
    ```  
  
-   품질  
  
     새롭게 디자인된 단어 분리기는 테스트 결과 이전의 단어 분리기보다 형태소 분석 품질이 뛰어난 것으로 나타났습니다. 이는 재호출 정확성을 높입니다.  
  
-   다양한 언어에 대한 단어 분리기가 SQL Server에 포함되었으며 기본적으로 사용하도록 설정되어 있습니다.  
  
 SQL Server에 포함된 단어 분리기 및 형태소 분석기가 지원하는 언어 목록은 [sys.fulltext_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)를 참조하세요.  
  
  
### <a name="how-full-text-search-uses-the-name-of-the-column-level-language"></a>전체 텍스트 검색에서 열 수준 언어 이름을 사용하는 방식  
 전체 텍스트 인덱스를 만들 때는 각 열마다 유효한 언어 이름을 지정해야 합니다. 유효한 언어 이름이 [sys.fulltext_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) 카탈로그 뷰에서 반환되지 않을 경우 전체 텍스트 검색은 동일 언어군에서 가장 근접한 언어 이름이 있으면 이를 대신 사용합니다. 그렇지 않으면 중립 단어 분리기를 사용합니다. 이러한 대체 동작은 재호출 정확성에 영향을 줄 수 있습니다. 따라서 전체 텍스트 인덱스를 만들 때는 각 열마다 유효하고 사용 가능한 언어 이름을 지정하는 것이 가장 좋습니다.  
  
> [!NOTE]  
>  LCID는 **char** 또는 **nchar** 등의 전체 텍스트 인덱싱에 적합한 모든 데이터 형식에 대해 사용됩니다. **char**, **varchar** 또는 **text** 형식 열의 정렬 순서를 LCID로 식별된 언어와 다른 언어 설정으로 지정할 경우에도 이러한 행에 대한 전체 텍스트 인덱싱 및 쿼리를 수행하는 동안에는 LCID가 사용됩니다.  
  
  
##  <a name="word-breaking"></a><a name="breaking"></a> 단어 분리  
 단어 분리기는 특정 언어와 관련된 단어 경계에서 인덱싱되는 텍스트를 토큰화합니다. 따라서 단어 분리 동작은 각 언어마다 다릅니다. x라는 언어를 사용하여 {x, y 및 z}의 여러 언어를 인덱싱하는 경우 일부 동작에서 예상치 못한 결과가 발생할 수 있습니다. 예를 들어 언어에 따라 대시(-) 또는 쉼표(,)가 버려지는 단어 분리 요소이거나 그렇지 않을 수 있습니다. 또한 드문 경우지만 특정 단어가 다른 언어에서는 다른 형태소로 분류되어 예상치 못한 형태소 분석 동작이 발생할 수도 있습니다. 예를 들어 영어에서는 일반적으로 공백이나 특정 형태의 문장 부호가 단어 경계로 사용되지만 독일어 등의 다른 언어에서는 단어 또는 문자 조합이 사용될 수 있습니다. 따라서 열의 행에 저장할 내용의 언어에 해당하는 열 수준 언어를 선택해야 합니다.  
  
### <a name="western-languages"></a>서구 언어  
 서구 어군의 경우 열에 저장할 내용의 언어가 무엇인지 확실하지 않거나 둘 이상의 언어로 된 내용을 저장하려는 경우에는 일반적으로 열에 저장할 내용의 언어 중 가장 복잡한 언어의 단어 분리기를 사용하는 것이 좋습니다. 예를 들어 단일 열에 영어, 스페인어 및 독일어 내용을 저장하려는 경우가 있습니다. 이러한 세 가지 서구 언어는 단어 분리 패턴이 매우 비슷하지만 이 중에서도 독일어 패턴이 가장 복잡합니다. 따라서 이 경우에는 영어와 스페인어 텍스트까지 올바르게 처리할 수 있는 독일어 단어 분리기를 사용하는 것이 좋습니다. 반대로 영어 단어 분리기는 독일어의 복합어 때문에 독일어 텍스트를 완전하게 처리할 수 없습니다.  
  
 한 언어군에서 가장 복잡한 언어의 단어 분리기를 사용한다고 해서 반드시 이러한 언어군의 모든 언어를 완전하게 인덱싱할 수 있다는 것은 아닙니다. 가장 복잡한 단어 분리기라도 다른 언어로 쓰인 텍스트를 제대로 처리하지 못할 수 있습니다.  
  
  
### <a name="non-western-languages"></a>동구 언어  
 일본어, 중국어 및 힌디어와 같은 동구 언어의 경우 언어적인 차이 때문에 위와 같은 방법이 반드시 효과가 있다고 보기는 어렵습니다. 동구 언어의 경우에는 다음과 같은 방법 중 하나를 고려해 보십시오.  
  
-   언어군이 다른 언어의 경우  
  
     스페인어 및 일본어와 같이 열에 포함된 언어가 완전히 다른 경우 각 언어 내용을 서로 다른 열에 저장하는 방법을 고려해 보십시오. 이렇게 하면 열마다 해당 언어와 관련된 단어 분리기를 사용할 수 있습니다. 이 방법을 사용하면 쿼리 단계에서 쿼리 언어를 알 수 없는 경우에 올바른 행 또는 문서를 찾을 수 있도록 두 열에 대해 쿼리를 실행해야 할 수도 있습니다.  
  
-   이진 내용의 경우(예: Microsoft Word 문서)  
  
     인덱싱된 내용이 **binary** 형식인 경우 전체 텍스트 검색 필터는 텍스트 내용을 단어 분리기로 보내기 위해 처리할 때 이진 파일 내에 있는 특정 언어 태그를 인식할 수 있습니다. 이 경우 인덱싱 단계에서 필터가 문서 전체 또는 문서 섹션의 정확한 LCID를 내보냅니다. 그런 다음 전체 텍스트 엔진이 이 LCID를 통해 적합한 언어의 단어 분리기를 호출합니다. 하지만 여러 언어 내용을 인덱싱한 후에는 내용이 올바르게 인덱싱되었는지를 확인하는 것이 좋습니다.  
  
-   일반 텍스트 내용의 경우  
  
     내용이 일반 텍스트로 구성된 경우 **xml** 데이터 형식으로 변환하여 특정 문서 전체 또는 문서 섹션에 해당하는 언어를 나타내는 언어 태그를 추가할 수 있습니다. 하지만 이렇게 하려면 전체 텍스트 인덱싱 전에 해당 언어를 알아야 합니다.  
  
  
##  <a name="stemming"></a><a name="stemming"></a> 형태소 분석  
 열 수준 언어를 선택할 때는 형태소 분석도 고려해야 합니다. 전체 텍스트 쿼리의 *형태소 분석* 이란 특정 언어로 된 한 단어의 모든 형태소(굴절형)를 검색하는 프로세스를 말합니다. 일반적인 단어 분리기를 사용하여 몇 가지 언어를 처리하는 경우 형태소 분석 프로세스는 열에 대해 지정된 언어에 대해서만 작동하고, 열의 다른 언어에 대해서는 작동하지 않습니다. 예를 들어 독일어 형태소 분석기는 영어 또는 스페인어 등에는 작동하지 않습니다. 이는 쿼리 단계에서 선택한 언어에 따라 회수에 영향을 줄 수 있습니다.  
  
  
##  <a name="effect-of-column-type-on-full-text-search"></a><a name="type"></a> 전체 텍스트 검색에 대한 열 유형의 영향  
 언어 선택에서 또 다른 고려 사항은 데이터 표현 방법과 관련이 있습니다. **varbinary(max)** 열에 저장되지 않은 데이터에 대해서는 특수 필터링이 수행되지 않습니다. 일반적으로 텍스트는 있는 그대로 단어 분리기 구성 요소를 통과합니다.  
  
 또한 단어 분리기는 주로 문자 텍스트를 처리합니다. 따라서 HTML과 같은 표시 유형이 텍스트에 포함되어 있을 경우 인덱싱 및 검색 중에 언어 정확도가 떨어질 수 있습니다. 이 경우 두 가지 방법이 있습니다. 이 중 권장되는 방법은 단순히 텍스트 데이터를 **varbinary(max)** 열에 저장하고 해당 문서 유형을 필터링하도록 지정하는 것입니다. 이 방법을 선택할 수 없으면 중립 단어 분리기를 사용하고 가능한 경우 의미 없는 단어 목록에 HTML의 'br'과 같은 표시 데이터를 추가할 수 있습니다.  
  
> [!NOTE]  
>  중립 언어를 지정하면 언어 기반 형태소 분석은 적용되지 않습니다.  
  
  
##  <a name="specifying-a-non-default-column-level-language-in-a-full-text-query"></a><a name="nondef"></a> 전체 텍스트 쿼리에서 기본이 아닌 열 수준 언어 지정  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 전체 텍스트 검색을 수행하면 전체 텍스트 절에 포함된 각 열에 대해 지정된 언어를 사용하여 쿼리 용어가 구문 분석됩니다. 이러한 동작을 무시하려면 쿼리 단계에서 기본 언어가 아닌 다른 언어를 지정합니다. 리소스가 설치되어 있는 지원 언어의 경우 *CONTAINS* , [CONTAINSTABLE](../../t-sql/queries/contains-transact-sql.md), [FREETEXT](../../relational-databases/system-functions/containstable-transact-sql.md)또는 [FREETEXTTABLE](../../t-sql/queries/freetext-transact-sql.md)쿼리의 LANGUAGE [language_term](../../relational-databases/system-functions/freetexttable-transact-sql.md) 절을 사용하여 쿼리 용어의 단어 분리, 형태소 분석, 동의어 사전 및 중지 단어 처리에 사용되는 언어를 지정할 수 있습니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [CONTAINS&#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [FREETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [검색 필터 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [sp_fulltext_service&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [sys.fulltext_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  
