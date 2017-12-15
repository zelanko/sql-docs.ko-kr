---
title: "검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
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
caps.latest.revision: "89"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba873b9ae0f29caa7acc85e5d5daed8dcbfd22a9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="configure-and-manage-word-breakers-and-stemmers-for-search"></a>검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] 단어 분리기와 형태소 분석기는 모든 전체 텍스트 인덱싱된 데이터에 대해 언어 분석을 수행합니다. 언어 분석에서는 다음 두 작업을 수행합니다.

-   **단어 경계 찾기(단어 분리)**. *단어 분리기*는 해당 언어의 어휘 규칙을 기준으로 단어의 경계를 결정하는 개별 단어를 식별합니다. 각 단어( *토큰*이라고도 함)는 압축된 표현으로 크기를 줄여 전체 텍스트 인덱스에 삽입됩니다.

-   **켤레 동사(형태소 분석)**. *형태소 분석기* 는 해당 언어의 규칙에 따라 특정 단어의 굴절형을 생성합니다. 예를 들어 "running", "ran" 및 "runner"는 "run"이라는 단어의 여러 가지 형태입니다.

## <a name="word-breakers-and-stemmers-are-language-specific"></a>단어 분리기 및 형태소 분석기는 언어별로 제공됩니다.

단어 분리기와 형태소 분석기는 언어별로 제공되며 언어 분석 규칙은 언어마다 다릅니다. 언어별 단어 분리기는 해당 언어에 맞는 보다 정확한 결과를 반환할 수 있습니다.

SQL Server에서 지원하는 모든 언어에 대해 제공되는 단어 분리기 및 형태소 분석기를 사용하기 위해 일반적으로 다른 작업을 수행할 필요가 없습니다.

-   해당 언어군의 단어 분리기만 있고 특정 하위 언어의 단어 분리기가 없으면 주 언어가 사용됩니다. 예를 들어 프랑스어 단어 분리기를 사용하여 프랑스어(캐나다) 텍스트를 처리합니다.
-   특정 언어의 단어 분리기를 사용할 수 없으면 중립 단어 분리기가 사용됩니다. 중립 단어 분리기를 사용하면 공백 및 문장 부호 표시와 같은 중립 문자에서 단어가 분리됩니다.

## <a name="get-the-list-of-supported-languages"></a>지원되는 언어 목록 가져오기

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색에서 지원하는 언어 목록을 보려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다. 이 목록에 언어가 있으면 단어 분리기가 해당 언어에 대해 등록되어 있음을 나타냅니다. 
  
```tsql
SELECT * FROM sys.fulltext_languages
```

##  <a name="register"></a> 등록된 단어 분리기 목록 가져오기

전체 텍스트 검색에서 언어에 대한 단어 분리기를 사용하려면 단어 분리기가 등록되어 있어야 합니다. 단어 분리기가 등록되면 형태소 분석기, 의미 없는 단어(중지 단어) 및 동의어 사전 파일과 같은 관련 언어의 리소스도 전체 텍스트 인덱싱 및 쿼리 작업에 사용할 수 있습니다.

등록된 단어 분리기 구성 요소 목록을 보려면 다음 문을 사용합니다.

```tsql
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```

추가 옵션 및 추가 정보는 [sp_help_fulltext_system_components&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)를 참조하세요.
 
## <a name="if-you-add-or-remove-a-word-breaker"></a>단어 분리기를 추가 또는 제거하는 경우  
단어 분리기를 추가, 제거 또는 변경한 경우에는 전체 텍스트 인덱싱 및 쿼리에서 지원되는 Microsoft Windows LCID(로캘 ID) 목록을 새로 고쳐야 합니다. 자세한 내용은 [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)을 참조하세요.  
  
##  <a name="default"></a> 기본 전체 텍스트 언어 옵션 설정  
 지역화된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전의 경우 일치하는 언어가 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 **default full-text language** 옵션을 서버 언어로 설정합니다. 지역화되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전의 경우 **default full-text language** 옵션이 영어입니다.  
  
 전체 텍스트 인덱스를 만들거나 변경할 때는 각 전체 텍스트 인덱싱된 열마다 다른 언어를 지정할 수 있습니다. 열에 언어를 지정하지 않으면 기본적으로 구성 옵션 **default full-text language**의 값이 사용됩니다.  
  
> [!NOTE]  
>  쿼리에 LANGUAGE 옵션을 지정하지 않은 경우 하나의 전체 텍스트 쿼리 함수 절에 있는 모든 열은 동일한 언어를 사용해야 합니다. 쿼리 중인 전체 텍스트 인덱싱된 열의 언어에 따라 전체 텍스트 쿼리 조건자([CONTAINS](../../t-sql/queries/contains-transact-sql.md) 및 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) 및 함수([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 및 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md))의 인수에 대해 수행되는 언어 분석이 결정됩니다.  
  
##  <a name="lang"></a> 인덱싱된 열에 대한 언어 선택  
 전체 텍스트 인덱스를 만들 때는 각 인덱싱된 열에 대해 언어를 지정하는 것이 좋습니다. 열에 언어를 지정하지 않으면 시스템 기본 언어가 사용됩니다. 열의 언어에 따라 해당 열을 인덱싱하는 데 사용되는 단어 분리기와 형태소 분석기가 결정됩니다. 또한 지정된 언어의 동의어 사전 파일이 해당 열에 대한 전체 텍스트 쿼리에 사용됩니다.  
  
 전체 텍스트 인덱스를 만들기 위해 열 언어를 선택할 때 고려할 몇 가지 사항이 있습니다. 이러한 고려 사항은 전체 텍스트 엔진으로 텍스트를 토큰화한 다음 인덱싱하는 방법과 관련이 있습니다. 자세한 내용은 [전체 텍스트 인덱스 생성 시 언어 선택](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)을 참조하세요.  
  
특정 열의 단어 분리기 언어를 보려면 다음 문을 실행합니다.
   
```tsql 
SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;
```  

추가 옵션 및 추가 정보는 [sys.fulltext_index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)를 참조하세요.

##  <a name="tshoot"></a> 단어 분리 시간 초과 오류 해결  
 단어 분리 시간 초과 오류는 다양한 상황에서 발생할 수 있습니다. 이러한 상황과 각 상황에서의 대처 방법에 대한 자세한 내용은 [MSSQLSERVER_30053](https://msdn.microsoft.com/en-us/library/cc879279.aspx)을 참조하세요.

### <a name="info-about-the-mssqlserver30053-error"></a>MSSQLSERVER_30053 오류에 대한 정보
  
|속성|Value|
|-|-|
|제품 이름|SQL Server|  
|이벤트 ID|30053|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|메시지 텍스트|전체 텍스트 쿼리 문자열의 단어 분리 작업이 시간을 초과했습니다. 단어 분리기에서 전체 텍스트 쿼리 문자열을 처리하는 데 오랜 시간이 걸리거나 서버에서 많은 쿼리가 실행되는 경우 이 오류가 발생할 수 있습니다. 부하를 줄여 쿼리를 다시 실행하십시오.|  
  
#### <a name="explanation"></a>설명  
 다음과 같은 경우 단어 분리 시간 초과 오류가 발생할 수 있습니다.  
  
-   쿼리 언어용 단어 분리기가 올바르지 않게 구성된 경우. 해당 레지스트리 설정이 올바르지 않은 경우가 이에 해당합니다.  
  
-   특정 쿼리 문자열에 대해 단어 분리기가 제대로 작동하지 않는 경우  
  
-   특정 쿼리 문자열에 대해 단어 분리기가 너무 많은 데이터를 반환하는 경우 데이터가 지나치게 많으면 버퍼 오버런 공격으로 간주되어 단어 분리 서비스를 호스팅하는 필터 데몬 프로세스(fdhost.exe)가 종료될 수 있습니다.  
  
-   필터 데몬 프로세스 구성이 올바르지 않은 경우  
  
     가장 일반적인 구성 문제는 암호 만료나 필터 데몬 계정이 로그온하지 못하도록 하는 도메인 정책입니다.  
  
-   서버 인스턴스에서 실행되는 쿼리 작업의 양이 너무 많은 경우. 단어 분리기에서 전체 텍스트 쿼리 문자열을 처리하는 데 오랜 시간이 걸리거나 서버에서 많은 쿼리가 실행되는 경우가 이에 해당됩니다. 이는 가능성이 가장 낮은 원인입니다.  
  
#### <a name="user-action"></a>사용자 동작  
 다음과 같이 시간 초과 문제의 가능한 원인에 적합한 사용자 동작을 선택합니다.  
  
|예상 원인|사용자 동작|  
|--------------------|-----------------|  
|쿼리 언어용 단어 분리기가 올바르지 않게 구성된 경우|타사 단어 분리기를 사용할 경우 운영 체제에 올바르지 않게 등록되어 있을 수 있습니다. 이 경우 단어 분리기를 다시 등록하십시오. 자세한 내용은 [검색에 사용된 단어 분리기를 이전 버전으로 되돌리기](revert-the-word-breakers-used-by-search-to-the-previous-version.md)를 참조하세요.|  
|특정 쿼리 문자열에 대해 단어 분리기가 제대로 작동하지 않는 경우|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 단어 분리기의 경우 Microsoft 고객 서비스 지원 센터에 문의하십시오.|  
|특정 쿼리 문자열에 대해 단어 분리기가 너무 많은 데이터를 반환하는 경우|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 단어 분리기의 경우 Microsoft 고객 서비스 지원 센터에 문의하십시오.|  
|필터 데몬 프로세스 구성이 올바르지 않은 경우|현재 암호를 사용 중이고 도메인 정책에서 필터 데몬 계정 로그온을 차단하고 있는지 확인하십시오.|  
|서버에서 실행되는 쿼리 작업의 양이 너무 많은 경우|부하를 줄여 쿼리를 다시 실행하십시오.|  

##  <a name="impact"></a> 업데이트된 단어 분리기의 영향 이해  
 각 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 일반적으로 더욱 효과적인 언어 규칙이 있고 이전 단어 분리기보다 정확한 차세대 단어 분리기가 포함되어 있습니다. 경우에 따라 새로운 단어 분리기가 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 가져온 전체 텍스트 인덱스의 단어 분리기와 약간 다르게 동작할 수도 있습니다.
 
이는 데이터베이스를 현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드한 상태에서 전체 텍스트 카탈로그를 가져온 경우에 중요합니다. 이제 전체 텍스트 카탈로그의 전체 텍스트 인덱스에서 사용되는 하나 이상의 언어를 새로운 단어 분리기와 연결할 수 있습니다. 자세한 내용은 [전체 텍스트 검색 업그레이드](../../relational-databases/search/upgrade-full-text-search.md)를 참조하세요.  
  

## <a name="see-also"></a>참고 항목  
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)    
 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 
  
