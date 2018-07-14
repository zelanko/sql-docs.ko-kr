---
title: 전체 텍스트 검색의 동작 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- behavior changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: 573444e8-51bc-4f3d-9813-0037d2e13b8f
caps.latest.revision: 39
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f136a7016e1b17248a3b547da0561cc3d4b30c68
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233803"
---
# <a name="behavior-changes-to-full-text-search"></a>전체 텍스트 검색의 동작 변경
  이 항목에서는 전체 텍스트 검색의 동작 변경 내용에 대해 설명합니다. 동작 변경 내용은 이전 버전의 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 와 비교해서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 기능이 작동하고 상호 작용하는 방법에 영향을 줍니다.  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>전체 텍스트 검색의 동작 변경 내용[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 향후 정보 제공 예정  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>전체 텍스트 검색의 동작 변경 내용[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]는 미국 영어(LCID 1033) 및 영국 영어(LCID 2057)에 대해 새로운 버전의 단어 분리기 및 형태소 분석기를 설치합니다. 하지만 이전 동작을 유지하려는 경우 이러한 구성 요소의 이전 버전으로 전환할 수 있습니다. 자세한 내용은 [미국 영어 및 영국 영어에 사용되는 단어 분리기 변경](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)을 참조하세요.  
  
### <a name="new-word-breakers-and-stemmers-installed"></a>새 단어 분리기 및 형태소 분석기 설치됨  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]는 전체 텍스트 검색 및 의미 체계 검색에서 사용되는 모든 단어 분리기 및 형태소 분석기를 업데이트합니다. 인덱스 내용과 쿼리 결과 사이에 일관성을 유지하기 위해 기존 전체 텍스트 인덱스를 다시 채우는 것이 좋습니다.  
  
1.  영어에 대한 새로운 단어 분리기가 있습니다. 이전 동작을 유지해야 하는 경우 [Change the Word Breaker Used for US English and UK English](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)을 참조하십시오.  
  
2.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이전 릴리스에 포함된 덴마크어, 폴란드어 및 터키어에 대한 타사 단어 분리기는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 구성 요소로 대체되었습니다. 새 구성 요소는 기본적으로 활성화됩니다.  
  
3.  체코어 및 그리스어에 대한 새로운 단어 분리기가 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 전체 텍스트 검색의 이전 릴리스에는 이 두 언어에 대한 지원이 포함되지 않았습니다.  
  
### <a name="behavior-changes-of-new-word-breakers-and-stemmers"></a>새 단어 분리기 및 형태소 분석기의 동작 변경  
 전체 텍스트 인덱스를 채우고 쿼리할 때 새 구성 요소는 이전 구성 요소와 다른 결과를 반환할 수 있습니다. 다음 표에서는 영어 결과에서 예상할 수 있는 몇 가지 차이점을 보여 줍니다.  
  
 단어 분석기와 형태소 분석기의 이전 동작을 유지해야 하는 경우 다음 항목을 참조하십시오.  
  
-   [미국 영어 및 영국 영어에 사용되는 단어 분리기 변경](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
-   [검색에 사용된 단어 분리기를 이전 버전으로 되돌리기](../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
 경우에 따라 새 구성 요소는 *더 많은* 결과를 반환합니다.  
  
|**용어**|**이전 단어 분리기 및 형태소 분석기를 사용 하 여 결과**|**새 단어 분리기 및 형태소 분석기를 사용 하 여 결과**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|cat-dog|cat<br /><br /> dog|cat<br /><br /> cat-dog<br /><br /> dog|  
|cat@dog.com|cat<br /><br /> com<br /><br /> dog|cat<br /><br /> cat@dog.com<br /><br /> com<br /><br /> dog|  
|12/11/2011<br /><br /> *(여기서 용어는 날짜)*|12/11/2011<br /><br /> dd20111211|11<br /><br /> 12<br /><br /> 12/11/2011<br /><br /> 2011<br /><br /> dd20111211|  
  
 경우에 따라 새 구성 요소는 *유사한* 결과를 반환합니다.  
  
|**용어**|**이전 단어 분리기 및 형태소 분석기를 사용 하 여 결과**|**새 단어 분리기 및 형태소 분석기를 사용 하 여 결과**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|100$|100$<br /><br /> nn100$|100$<br /><br /> nn100usd|  
|022|022<br /><br /> nn022|022<br /><br /> nn22|  
|10:49AM<br /><br /> *(여기서 용어는 한 번)*|10:49AM<br /><br /> tt1049|10:49AM<br /><br /> tt24104900|  
  
 경우에 따라 새 구성 요소는 *더 적은* 결과 또는 응용 프로그램에서 예상되지 않을 수 있는 결과를 반환합니다.  
  
|**용어**|**이전 단어 분리기 및 형태소 분석기를 사용 하 여 결과**|**새 단어 분리기 및 형태소 분석기를 사용 하 여 결과**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|jěˊÿqℭžl<br /><br /> *(여기서 용어는 하지 유효한 영어 문자가)*|‘jěˊÿｑℭžl’|je yq zl|  
|table's|table’s<br /><br /> 테이블|table’s|  
|cat-|cat<br /><br /> cat-|cat|  
|v-z *(여기서 v 및 z는 의미 없는 단어)*|*(결과 없음)*|v-z|  
|$100 000 USD|$100<br /><br /> 000<br /><br /> nn000<br /><br /> nn100$<br /><br /> usd|$100 000 USD<br /><br /> nn100000usd|  
|beautiful U.S land|beautiful<br /><br /> land<br /><br /> u.s<br /><br /> us|beautiful<br /><br /> land|  
|Mt. Kent and Mt Challenger|challenger<br /><br /> kent<br /><br /> mt<br /><br /> Mt.|mt<br /><br /> kent<br /><br /> challenger|  
  
## <a name="behavior-changes-in-full-text-search-in-sql-server-2008"></a>SQL Server 2008 전체 텍스트 검색의 동작 변경 내용  
 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 이상 버전에서는 전체 텍스트 엔진은 서버 쿼리 및 저장소 엔진 인프라의 일부로 관계형 데이터베이스에 데이터베이스 서비스로 통합 되어 있습니다. 새로운 전체 텍스트 검색 아키텍처는 다음과 같은 목표를 달성합니다.  
  
-   저장과 관리가 통합-전체 텍스트 검색의 내재 된 저장소 및 관리 기능을 사용 하 여 직접 통합 되었습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], MSFTESQL 서비스는 더 이상 없습니다.  
  
    -   전체 텍스트 인덱스가 파일 시스템이 아닌 데이터베이스 파일 그룹 내에 저장됩니다. 데이터베이스에 대한 백업 만들기와 같은 관리 작업은 전체 텍스트 인덱스에 자동으로 영향을 줍니다.  
  
    -   이제 전체 텍스트 카탈로그는 파일 그룹에 속하지 않는 가상 개체이며, 전체 텍스트 인덱스의 그룹을 나타내는 논리적인 개념입니다. 따라서 여러 가지 카탈로그 관리 기능이 더 이상 사용되지 않으며, 이로 인해 일부 기능이 크게 변경되었습니다. 자세한 내용은 참조 하세요. [SQL Server 2014 데이터베이스 엔진 기능의 사용 되지 않음](deprecated-database-engine-features-in-sql-server-2016.md) 하 고 [전체 텍스트 검색의 주요 변경 내용](breaking-changes-to-full-text-search.md)합니다.  
  
        > [!NOTE]  
        >  전체 텍스트 카탈로그를 지정하는 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] DDL 문은 올바르게 작동합니다.  
  
-   쿼리 처리가 통합되었습니다. 새로운 전체 텍스트 검색 쿼리 프로세서는 데이터베이스 엔진의 일부이며 SQL Server 쿼리 프로세서와 완벽하게 통합되어 있습니다. 따라서 쿼리 최적화 프로그램에서 전체 텍스트 쿼리 조건자를 인식하여 자동으로 최대한 효율적으로 실행합니다.  
  
-   관리 및 문제 해결 기능이 향상되었습니다. 통합된 전체 텍스트 검색에서는 전체 텍스트 인덱스, 특정 단어 분리기의 출력, 중지 단어 구성 등의 검색 구조를 분석하는 데 도움이 되는 도구를 제공합니다.  
  
-   의미 없는 단어 및 의미 없는 단어 파일 대신 중지 단어 및 중지 목록이 사용됩니다. 중지 목록은 중지 단어에 대한 관리 태스크를 지원하고 서로 다른 서버 인스턴스와 환경 사이의 무결성을 높여 주는 데이터베이스 개체입니다. 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.  
  
-   [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 및 이후 버전에는 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]에 있는 언어 중 다수에 대한 새로운 단어 분리기가 포함되어 있습니다. 영어, 한국어, 태국어 및 중국어(모든 형태 포함)에 대한 단어 분리기만 동일하게 유지됩니다. 다른 언어의 전체 텍스트 카탈로그를 가져온 경우에 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 데이터베이스를 업그레이드 된 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그의 전체 텍스트 인덱스에 사용 되는 언어 중 하나 이상 연결 될 수 있습니다 새 단어 분리기를 사용 하 여 또는 수는 단어 분리기는 가져온된 단어 분리기에서와 약간 다르게 작동 합니다. 쿼리와 전체 텍스트 인덱스 내용 간에 일관성을 유지 하는 방법에 대 한 자세한 내용은 참조 하세요. [전체 텍스트 검색 업그레이드](../relational-databases/search/upgrade-full-text-search.md)합니다.  
  
-   새로운 FDHOST Launcher(MSSQLFDLauncher) 서비스가 추가되었습니다. 자세한 내용은 [전체 텍스트 검색 시작](../relational-databases/search/get-started-with-full-text-search.md)합니다.  
  
-   전체 텍스트 인덱싱 사용 하 여 작동는 [FILESTREAM](../relational-databases/blob/filestream-sql-server.md) 열에서와 동일한 방식에서를 `varbinary(max)` 열입니다. FILESTREAM 테이블에는 각 FILESTREAM BLOB에 대한 파일 이름 확장명을 포함하는 열이 있어야 합니다. 자세한 내용은 [전체 텍스트 검색을 사용 하 여 쿼리](../relational-databases/search/query-with-full-text-search.md)를[필터 구성 및 관리 검색에 대 한](../relational-databases/search/configure-and-manage-filters-for-search.md), 및 [sys.fulltext_document_types &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
     전체 텍스트 엔진은 FILESTREAM BLOB의 내용을 인덱싱합니다. 이미지와 같은 인덱싱 파일은 유용하지 않을 수도 있습니다. FILESTREAM BLOB이 업데이트되면 인덱스가 다시 작성됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [전체 텍스트 검색] ((.. / relational-databases/search/full-text-search.md)   
 [전체 텍스트 Search 이전 버전과 호환성](../../2014/database-engine/full-text-search-backward-compatibility.md)   
 [전체 텍스트 검색 업그레이드](../relational-databases/search/upgrade-full-text-search.md)   
 [전체 텍스트 검색 시작](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
