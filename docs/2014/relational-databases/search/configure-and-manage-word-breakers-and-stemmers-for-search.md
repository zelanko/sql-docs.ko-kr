---
title: 검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- languages [full-text search]
- full-text search [SQL Server], stemmers
- linguistic analysis [full-text search]
- full-text indexes [SQL Server], linguistic analysis
- full-text search [SQL Server], word breakers
- default full-text language option
- stemmers [full-text search]
- conjugating verbs [full-text search]
- word breakers [full-text search]
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
caps.latest.revision: 88
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4c3bfb07ca9730b8c03cb56f07464355c392bda6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187376"
---
# <a name="configure-and-manage-word-breakers-and-stemmers-for-search"></a>검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리
  단어 분리기와 형태소 분석기는 모든 전체 텍스트 인덱싱된 데이터에 대해 언어 분석을 수행합니다. 언어 분석에는 단어 경계 찾기(단어 분리) 및 동사 변화(형태소 분석)가 있습니다. 단어 분리기와 형태소 분석기는 언어별로 제공되며 언어 분석 규칙은 언어마다 다릅니다. 지정된 언어에 대해 *단어 분리기* 는 해당 언어의 어휘 규칙을 기준으로 단어의 경계를 결정하는 개별 단어를 식별합니다. 각 단어( *토큰*이라고도 함)는 압축된 표현으로 크기를 줄여 전체 텍스트 인덱스에 삽입됩니다. *형태소 분석기* 는 해당 언어의 규칙에 따라 특정 단어의 굴절형을 생성합니다. 예를 들어 "running", "ran" 및 "runner"는 "run"이라는 단어의 여러 가지 형태입니다.  
  
 언어별 단어 분리기를 사용하면 해당 언어에 맞는 비교적 정확한 결과를 반환할 수 있습니다. 해당 언어군의 단어 분리기만 있고 특정 하위 언어의 단어 분리기가 없으면 주 언어가 사용됩니다. 예를 들어 프랑스어 단어 분리기를 사용하여 프랑스어(캐나다) 텍스트를 처리합니다. 특정 언어의 단어 분리기를 사용할 수 없으면 중립 단어 분리기가 사용됩니다. 중립 단어 분리기를 사용하면 공백 및 문장 부호 표시와 같은 중립 문자에서 단어가 분리됩니다.  
  
##  <a name="register"></a> 단어 분리기 등록  
 특정 언어의 단어 분리기를 사용하려면 등록해야 합니다. 단어 분리기가 등록되면 형태소 분석기, 의미 없는 단어(중지 단어) 및 동의어 사전 파일과 같은 관련 언어의 리소스도 전체 텍스트 인덱싱 및 쿼리 작업에 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 현재 단어 분리기가 등록된 언어 목록을 보려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하십시오.  
  
 SELECT * FROM sys.fulltext_languages  
  
 단어 분리기를 추가, 제거 또는 변경한 경우에는 전체 텍스트 인덱싱 및 쿼리에서 지원되는 Microsoft Windows LCID(로캘 ID) 목록을 새로 고쳐야 합니다. 자세한 내용은 [등록된 필터와 단어 분리기 보기 및 변경](view-or-change-registered-filters-and-word-breakers.md)을 참조하세요.  
  
##  <a name="default"></a> 기본 전체 텍스트 언어 옵션 설정  
 지역화 된 버전에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 설치는 `default full-text language` 적절 한 일치 하는 경우 옵션을 서버 언어로 합니다. 지역화 되지 않은 버전의 호스트용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `default full-text language` 옵션이 영어입니다.  
  
 전체 텍스트 인덱스를 만들거나 변경할 때는 각 전체 텍스트 인덱싱된 열마다 다른 언어를 지정할 수 있습니다. 열에 언어를 지정하지 않으면 기본적으로 구성 옵션 `default full-text language`의 값이 사용됩니다.  
  
> [!NOTE]  
>  쿼리에 LANGUAGE 옵션을 지정하지 않은 경우 하나의 전체 텍스트 쿼리 함수 절에 있는 모든 열은 동일한 언어를 사용해야 합니다. 쿼리 중인 전체 텍스트 인덱싱된 열의 언어에 따라 전체 텍스트 쿼리 조건자([CONTAINS](/sql/t-sql/queries/contains-transact-sql) 및 [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)) 및 함수([CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 및 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql))의 인수에 대해 수행되는 언어 분석이 결정됩니다.  
  
##  <a name="lang"></a> 인덱싱된 열에 대 한 언어 선택  
 전체 텍스트 인덱스를 만들 때는 각 인덱싱된 열에 대해 언어를 지정하는 것이 좋습니다. 열에 언어를 지정하지 않으면 시스템 기본 언어가 사용됩니다. 열의 언어에 따라 해당 열을 인덱싱하는 데 사용되는 단어 분리기와 형태소 분석기가 결정됩니다. 또한 지정된 언어의 동의어 사전 파일이 해당 열에 대한 전체 텍스트 쿼리에 사용됩니다.  
  
 전체 텍스트 인덱스를 만들기 위해 열 언어를 선택할 때 고려할 몇 가지 사항이 있습니다. 이러한 고려 사항은 전체 텍스트 엔진으로 텍스트를 토큰화한 다음 인덱싱하는 방법과 관련이 있습니다. 자세한 내용은 [전체 텍스트 인덱스 생성 시 언어 선택](choose-a-language-when-creating-a-full-text-index.md)을 참조하세요.  
  
 **열의 단어 분리기 언어를 보려면**  
  
-   [전체 텍스트 인덱스 관리](../indexes/indexes.md)  
  
-   [sys.fulltext_index_columns&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="info"></a> 단어 분리기에 대 한 정보 얻기  
 **단어 분리기, 동의어 사전 및 중지 목록 조합의 토큰화 결과 보기**  
  
-   [sys.dm_fts_parser&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
 **등록된 된 단어 분리기에 대 한 정보를 반환 하려면**  
  
-   [sp_help_fulltext_system_components&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql)  
  
##  <a name="tshoot"></a> 단어 분리 시간 초과 오류 해결  
 단어 분리 시간 초과 오류는 다양한 상황에서 발생할 수 있습니다. 이러한 상황과 각 상황에서의 대처 방법은 [MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md)을 참조하세요.  
  
##  <a name="impact"></a> 새로운 단어 분리기의 영향 이해  
 각 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 일반적으로 더욱 효과적인 언어 규칙이 있고 이전 단어 분리기보다 정확한 차세대 단어 분리기가 포함되어 있습니다. 경우에 따라 새로운 단어 분리기가 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 가져온 전체 텍스트 인덱스의 단어 분리기와 약간 다르게 동작할 수도 있습니다. 이는 데이터베이스를 현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드한 상태에서 전체 텍스트 카탈로그를 가져온 경우에 중요합니다. 이제 전체 텍스트 카탈로그의 전체 텍스트 인덱스에서 사용되는 하나 이상의 언어를 새로운 단어 분리기와 연결할 수 있습니다. 자세한 내용은 [전체 텍스트 검색 업그레이드](upgrade-full-text-search.md)를 참조하세요.  
  
 모든 단어 분리기의 전체 목록은 참조 하십시오. [sys.fulltext_languages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [sp_fulltext_service&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)   
 [sys.fulltext_languages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [전체 텍스트 검색 업그레이드](upgrade-full-text-search.md)  
  
  
