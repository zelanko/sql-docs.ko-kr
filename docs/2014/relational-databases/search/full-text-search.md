---
title: 전체 텍스트 검색 | Microsoft 문서
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
- full-text search [SQL Server]
ms.assetid: a0ce315d-f96d-4e5d-b4eb-ff76811cab75
caps.latest.revision: 47
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d419f7a018817656ba9bb5910a71e2c2f810ae87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093283"
---
# <a name="full-text-search"></a>전체 텍스트 검색
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 의 전체 텍스트 검색을 사용하면 사용자와 응용 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 문자 기반 데이터에 대해 전체 텍스트 쿼리를 실행할 수 있습니다. 테이블에 대해 전체 텍스트 쿼리를 실행하려면 먼저 데이터베이스 관리자가 해당 테이블에 대한 전체 텍스트 인덱스를 만들어야 합니다. 전체 텍스트 인덱스에는 테이블에 있는 하나 이상의 문자 기반 열이 포함됩니다. 이러한 열 데이터 형식 중 하나일 수: `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml`, 또는 `varbinary(max)` 및 FILESTREAM 합니다. 각 전체 텍스트 인덱스는 테이블의 열을 하나 이상 인덱싱하며, 각 열은 특정 언어를 사용할 수 있습니다.  
  
 전체 텍스트 쿼리는 영어와 일본어 같은 특정 언어의 규칙을 기준으로 단어와 구에 적용되어 전체 텍스트 인덱스의 텍스트 데이터에 대해 언어 검색을 수행합니다. 전체 텍스트 쿼리에는 간단한 단어와 구 또는 여러 형식의 단어나 구가 포함될 수 있습니다. 전체 텍스트 쿼리는 일치 항목( *적중*이라고도 함)이 하나 이상 있는 문서를 모두 반환합니다. 대상 문서가 전체 텍스트 쿼리에 지정된 모든 용어를 포함하며 일치하는 용어 사이의 거리와 같이 다른 모든 검색 조건과 일치할 때 일치 항목이 발생합니다.  
  
> [!NOTE]  
>  전체 텍스트 검색은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진의 선택적 구성 요소입니다. 자세한 내용은 참조 [SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server.md)합니다.  
  
##  <a name="benefits"></a> 전체 텍스트 검색을 사용한 어떻게 해야 합니까?  
 전체 텍스트 검색은 웹 사이트에서 항목을 검색하는 e-비즈니스, 법률 데이터 리포지토리에서 판례 기록을 검색하는 법률 회사 또는 저장된 이력서 중에서 작업 설명과 일치하는 이력서를 검색하는 인사 부서와 같은 다양한 비즈니스 시나리오에 적용할 수 있습니다. 전체 텍스트 검색의 기본적인 관리 및 개발 태스크는 비즈니스 시나리오에 관계없이 동일합니다. 그러나 특정 비즈니스 시나리오에서는 비즈니스 목표를 충족시키기 위해 전체 텍스트 인덱스 및 쿼리를 조정할 수 있습니다. 예를 들어 e-비즈니스의 경우 결과 순위 지정, 회수 정확성(전체 텍스트 쿼리에서 실제로 반환하는 기존 일치 항목 수) 또는 여러 언어 지원보다 성능 최대화가 더 중요할 수 있고 법률 회사의 경우 일치하는 모든 항목 반환(정보의*전체 회수* )이 가장 중요한 고려 사항일 수 있습니다.  
  
 [항목 내용](#top)  
  
###  <a name="queries"></a> 전체 텍스트 검색 쿼리  
 전체 텍스트 인덱스에 열을 추가한 후에는 사용자와 응용 프로그램이 해당 열의 텍스트에 대해 전체 텍스트 쿼리를 실행할 수 있습니다. 이러한 쿼리는 다음 중 하나를 검색할 수 있습니다.  
  
-   하나 이상의 특정 단어 또는 구(*단순 단어*)  
  
-   특정 텍스트로 시작하는 단어 또는 그러한 단어를 포함하는 구(*접두사 단어*)  
  
-   특정 단어의 굴절형(*생성 단어*)  
  
-   다른 단어나 구와 근접한 단어나 구(*근접 단어*)  
  
-   특정 단어의 동의어 형태(*동의어 사전*)  
  
-   가중치를 사용하는 단어나 구(*가중치 단어*)  
  
 전체 텍스트 쿼리는 대/소문자를 구분하지 않습니다. 예를 들어 "Aluminum" 또는 "aluminum"을 검색하면 동일한 결과가 반환됩니다.  
  
 전체 텍스트 쿼리는 일부 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 조건자(CONTAINS 및 FREETEXT) 및 함수(CONTAINSTABLE 및 FREETEXTTABLE) 집합을 사용합니다. 그러나 전체 텍스트 쿼리의 구조는 지정된 비즈니스 시나리오의 검색 목표에 따라 달라집니다. 예를 들어:  
  
-   e-비즈니스 - 웹 사이트에서 제품 검색:  
  
    ```  
    SELECT product_id   
    FROM products   
    WHERE CONTAINS(product_description, "Snap Happy 100EZ"  
        OR FORMSOF(THESAURUS,'Snap Happy')  
        OR '100EZ')   
    AND product_cost < 200 ;  
    ```  
  
-   채용 시나리오 - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하여 작업한 경험이 있는 지원자 검색:  
  
    ```  
    SELECT candidate_name,SSN   
    FROM candidates   
    WHERE CONTAINS(candidate_resume,"SQL Server") AND candidate_division = 'DBA';  
    ```  
  
 자세한 내용은 [전체 텍스트 검색을 사용한 쿼리](query-with-full-text-search.md)를 참조하세요.  
  
 [항목 내용](#top)  
  
###  <a name="like"></a> LIKE와 전체 텍스트 검색 비교  
 전체 텍스트 검색과 달리 [LIKE](/sql/t-sql/language-elements/like-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 조건자는 문자 패턴에 대해서만 적용됩니다. 또한 LIKE 조건자는 서식 있는 이진 데이터를 쿼리하는 데 사용할 수도 없습니다. 특히 구조화되지 않은 많은 텍스트 데이터에 대한 LIKE 쿼리는 동일한 데이터에 대한 전체 텍스트 쿼리보다 훨씬 느립니다. 수백만 개의 텍스트 데이터 행에 대해 LIKE 쿼리를 실행하면 결과가 반환되기까지 몇 분이 걸릴 수 있지만 같은 데이터에 대해 전체 텍스트 쿼리를 실행하면 반환되는 행 수에 따라 몇 초 내에 완료됩니다.  
  
 [항목 내용](#top)  
  
##  <a name="architecture"></a> 구성 요소 및 전체 텍스트 검색의 아키텍처  
 전체 텍스트 검색 아키텍처는 다음과 같은 프로세스로 구성됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로세스(sqlservr.exe).  
  
-   필터 데몬 호스트 프로세스(fdhost.exe).  
  
     보안상의 이유로 필터가 필터 데몬 호스트라는 개별 프로세스에 의해 로드됩니다. fdhost.exe 프로세스는 FDHOST Launcher 서비스(MSSQLFDLauncher)에 의해 만들어지고 FDHOST Launcher 서버 계정의 보안 자격 증명을 사용하여 실행됩니다. 따라서 전체 텍스트 인덱싱과 전체 텍스트 쿼리를 수행하려면 FDHOST Launcher 서비스를 실행해야 합니다. 이 서비스에 대한 서비스 계정을 설정하는 방법은 [전체 텍스트 필터 데몬 시작 관리자 서비스 계정 설정](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)을 참조하세요.  
  
 이러한 두 프로세스에는 전체 텍스트 검색 아키텍처의 구성 요소가 포함됩니다. 이러한 구성 요소 및 이들의 관계는 다음 그림에 요약되어 있습니다. 구성 요소는 이 그림 다음에 설명되어 있습니다.  
  
 ![전체 텍스트 검색 아키텍처](../../database-engine/media/ifts-arch.gif "full-text search architecture")  
  
 [항목 내용](#top)  
  
###  <a name="sqlprocess"></a> SQL Server 프로세스  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로세스는 전체 텍스트 검색에 다음 구성 요소를 사용합니다.  
  
-   **사용자 테이블.** 이 테이블은 전체 텍스트 인덱싱할 데이터를 포함합니다.  
  
-   **전체 텍스트 Gatherer.** 전체 텍스트 Gatherer는 전체 텍스트 탐색 스레드와 함께 작동합니다. 이 구성 요소는 전체 텍스트 카탈로그를 모니터링하고 전체 텍스트 인덱스 채우기를 예약 및 수행합니다.  
  
-   **동의어 사전 파일.** 이 파일은 검색어의 동의어를 포함합니다. 자세한 내용은 [전체 텍스트 검색에 사용할 동의어 사전 파일 구성 및 관리](configure-and-manage-thesaurus-files-for-full-text-search.md)를 참조하세요.  
  
-   **중지 목록 개체.** Stoplist 개체는 검색에 유용하지 않은 일반적인 단어의 목록을 포함합니다. 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.  
  
-   **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 쿼리 프로세서.** 쿼리 프로세서는 SQL 쿼리를 컴파일하고 실행합니다. SQL 쿼리에 전체 텍스트 검색 쿼리가 포함된 경우 해당 쿼리는 컴파일 및 실행 중에 전체 텍스트 엔진으로 전송됩니다. 쿼리 결과는 전체 텍스트 인덱스와 일치합니다.  
  
-   **전체 텍스트 엔진.** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 전체 텍스트 엔진은 쿼리 프로세서와 완전히 통합됩니다. 전체 텍스트 엔진은 전체 텍스트 쿼리를 컴파일하고 실행합니다. 쿼리 실행의 일부로 전체 텍스트 엔진은 동의어 사전 및 중지 목록에서 입력을 받을 수 있습니다.  
  
-   **인덱스 기록기(인덱서).** 인덱스 기록기는 인덱싱된 토큰을 저장하는 데 사용되는 구조를 만듭니다.  
  
-   **필터 데몬 관리자.** 필터 데몬 관리자는 전체 텍스트 엔진 필터 데몬 호스트의 상태를 모니터링합니다.  
  
 [항목 내용](#top)  
  
###  <a name="fdhostprocess"></a> 필터 데몬 호스트 프로세스  
 필터 데몬 호스트는 전체 텍스트 엔진에 의해 시작되는 프로세스로, 테이블 데이터의 액세스, 필터링 및 단어 분리, 그리고 쿼리 입력의 단어 분리 및 형태소 분석을 담당하는 다음과 같은 전체 텍스트 검색 구성 요소를 실행합니다.  
  
 필터 데몬 호스트의 구성 요소는 다음과 같습니다.  
  
-   **프로토콜 처리기.** 이 구성 요소는 부가적인 처리를 위해 메모리에서 데이터를 가져오며 지정된 데이터베이스의 사용자 테이블에 있는 데이터에 액세스합니다. 프로토콜 처리기가 수행해야 하는 기능 중 하나는 전체 텍스트 인덱싱되는 열에서 데이터를 수집하고 필요에 따라 필터링과 단어 분리기를 적용하는 필터 데몬 호스트에 이 데이터를 전달하는 것입니다.  
  
-   **필터.** 일부 데이터 형식은 필터링을 적용해야 `varbinary`, `varbinary(max)`, `image` 또는 `xml` 열의 데이터를 포함하여 문서의 데이터를 전체 텍스트 인덱싱할 수 있습니다. 지정된 문서에 사용되는 필터는 해당 문서 유형에 따라 다릅니다. 예를 들어 Microsoft Word(.doc) 문서, Microsoft Excel(.xls) 문서 및 XML(.xml) 문서에는 서로 다른 필터가 사용됩니다. 그러면 필터는 포함된 서식을 제거하고 텍스트와 텍스트 위치에 대한 정보를 유지하여 문서에서 텍스트 청크를 추출합니다. 결과는 텍스트 정보의 스트림입니다. 자세한 내용은 [고급 분석 확장 구성 및 관리](configure-and-manage-filters-for-search.md)를 참조하세요.  
  
-   **단어 분리기 및 형태소 분석기.** 단어 분리기는 지정된 언어의 어휘 규칙을 기준으로 단어 경계(*단어 분리*)를 찾는 언어별 구성 요소입니다. 각 단어 분리기는 동사를 변화시키고 활용 형태상의 확장을 수행하는 언어별 형태소 분석기 구성 요소와 연결됩니다. 인덱싱할 때 필터 데몬 호스트는 단어 분리기와 형태소 분석기를 사용하여 지정된 테이블 열의 텍스트 데이터에 대해 언어 분석을 수행합니다. 전체 텍스트 인덱스의 테이블 열과 연결된 언어에 따라 열을 인덱싱하는 데 사용되는 단어 분리기와 형태소 분석기가 결정됩니다. 자세한 내용은 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](configure-and-manage-word-breakers-and-stemmers-for-search.md)를 참조하세요.  
  
 [항목 내용](#top)  
  
##  <a name="processing"></a> 전체 텍스트 검색 처리  
 전체 텍스트 검색은 전체 텍스트 엔진을 통해 수행됩니다. 전체 텍스트 엔진은 인덱싱 지원과 쿼리 지원의 두 가지 역할을 수행합니다.  
  
###  <a name="indexing"></a> 전체 텍스트 인덱싱 프로세스  
 탐색이라고도 하는 전체 텍스트 채우기가 시작되면 전체 텍스트 엔진은 대용량 데이터 일괄 처리를 메모리에 밀어 넣고 필터 데몬 호스트에 알립니다. 호스트가 데이터를 필터링하고 데이터의 단어를 분리하며 변환된 데이터를 반전된 단어 목록으로 변환합니다. 그런 다음 전체 텍스트 검색은 변환된 데이터를 단어 목록에서 끌어오고 데이터를 처리하여 중지 단어를 제거하며 하나의 일괄 처리에 대한 단어 목록을 하나 이상의 반전된 인덱스를 통해 유지합니다.  
  
 에 저장 된 데이터를 인덱싱하는 경우는 `varbinary(max)` 또는 `image` 열, 구현 하는 필터는 **IFilter** 인터페이스, 해당 데이터에 대 한 지정 된 파일 형식에 따라 추출한 텍스트 (예를 들어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word). 필터 구성 요소에 필요한 일부 경우에는 `varbinary(max)`, 또는 `image` 데이터를 메모리에 밀어 넣는 대신 filterdata 폴더에 기록해 야 합니다.  
  
 수집된 텍스트 데이터는 처리 중에 단어 분리기를 통과하여 텍스트가 개별 토큰 또는 키워드로 분리됩니다. 토큰화에 사용되는 언어는 열 수준에서 지정되거나 필터 구성 요소로 `varbinary(max)`, `image` 또는 `xml` 데이터 내에서 식별할 수 있습니다.  
  
 추가 처리를 수행하여 중지 단어를 제거하고 전체 텍스트 인덱스나 인덱스 조각에 저장되기 전에 토큰을 정규화할 수도 있습니다.  
  
 채우기가 완료되면 인덱스 조각을 하나의 마스터 전체 텍스트 인덱스로 병합하는 최종 병합 프로세스가 실행됩니다. 이렇게 하면 많은 인덱스 조각 대신 마스터 인덱스만 쿼리하면 되기 때문에 쿼리 성능이 향상되며 개선된 평가 통계를 사용하여 관련성 등급을 지정할 수 있습니다.  
  
 [항목 내용](#top)  
  
###  <a name="querying"></a> 전체 텍스트 쿼리 프로세스  
 쿼리 프로세서는 쿼리의 전체 텍스트 부분을 처리하기 위해 전체 텍스트 엔진에 전달합니다. 전체 텍스트 엔진은 단어 분리를 수행하고 필요에 따라 동의어 사전 확장, 형태소 분석 및 중지 단어(의미 없는 단어) 처리도 수행합니다. 그러면 쿼리의 전체 텍스트 부분은 SQL 연산자 형식, 주로 STVF(스트리밍 테이블 반환 함수)로 표시됩니다. 쿼리를 실행하는 동안 이러한 STVF는 반전된 인덱스에 액세스하여 올바른 결과를 검색합니다. 결과는 이 시점에서 클라이언트에 반환되거나 추가로 처리된 후 클라이언트에 반환됩니다.  
  
 [항목 내용](#top)  
  
##  <a name="components"></a> 언어 구성 요소 및 전체 텍스트 검색의 언어 지원  
 전체 텍스트 검색에서 영어, 스페인어, 중국어, 일본어, 아랍어, 벵골어 및 힌디어를 포함하여 거의 50개의 언어를 지원합니다. 지원되는 전체 텍스트 언어의 전체 목록은 [sys.fulltext_languages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)를 참조하세요. 전체 텍스트 인덱스에 있는 각 열은 전체 텍스트 검색에서 지원하는 언어에 해당하는 Windows LCID(로캘 ID)와 연결됩니다. 예를 들어 LCID 1033은 영어(미국)에 해당하고 LCID 2057은 영어(영국)에 해당합니다. 지원되는 각 전체 텍스트 언어에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 해당 언어로 저장되는 전체 텍스트 데이터의 인덱싱 및 쿼리를 지원하는 언어 구성 요소를 제공합니다.  
  
 다음과 같은 언어별 구성 요소가 있습니다.  
  
-   **단어 분리기 및 형태소 분석기.** 단어 분리기는 지정된 언어의 어휘 규칙을 기준으로 단어 경계(*단어 분리*)를 찾습니다. 각 단어 분리기는 동일한 언어의 동사를 변화시키는 형태소 분석기와 연결됩니다. 자세한 내용은 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](configure-and-manage-word-breakers-and-stemmers-for-search.md)를 참조하세요.  
  
-   **중지 목록.** 중지 단어(의미 없는 단어라고도 함)의 기본 집합이 포함된 시스템 중지 목록이 제공됩니다. *중지 단어* 는 검색에 도움이 되지 않고 전체 텍스트 쿼리에서 무시되는 단어입니다. 예를 들어 영어 로캘의 경우 "a", "and", "is" 및 "the"와 같은 단어는 중지 단어로 간주됩니다. 일반적으로 하나 이상의 동의어 사전 파일과 중지 목록을 구성해야 합니다. 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.  
  
-   **동의어 사전 파일.** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 또한 각 전체 텍스트 언어에 대한 동의어 사전 파일뿐 아니라 전역 동의어 사전 파일도 설치합니다. 설치된 동의어 사전 파일은 기본적으로 비어 있지만 이러한 동의어 사전 파일을 편집하여 특정 언어 또는 비즈니스 시나리오에 대한 동의어를 정의할 수 있습니다. 전체 텍스트 데이터에 맞게 동의어 사전을 개발하면 해당 데이터에 대한 전체 텍스트 쿼리의 범위를 효과적으로 넓힐 수 있습니다. 자세한 내용은 [전체 텍스트 검색에 사용할 동의어 사전 파일 구성 및 관리](configure-and-manage-thesaurus-files-for-full-text-search.md)를 참조하세요.  
  
-   **필터(iFilters).**  `varbinary(max)`, `image` 또는 `xml` 데이터 형식의 문서를 인덱싱하려면 추가 처리를 수행하는 필터가 필요합니다. 필터는 문서 유형(.doc, .pdf, .xls, .xml 등)에 따라 달라야 합니다. 자세한 내용은 [고급 분석 확장 구성 및 관리](configure-and-manage-filters-for-search.md)를 참조하세요.  
  
 단어 분리기(및 형태소 분석기)와 필터는 필터 데몬 호스트 프로세스(fdhost.exe)에서 실행됩니다.  
  
 [항목 내용](#top)  
  
##  <a name="reltasks"></a> 관련 작업  
  
-   [전체 텍스트 검색 시작](get-started-with-full-text-search.md)  
  
-   전체 텍스트 쿼리 쓰기  
  
    -   [전체 텍스트 검색을 사용한 쿼리](query-with-full-text-search.md)  
  
    -   [NEAR를 사용하여 근접 단어 검색](search-for-words-close-to-another-word-with-near.md)  
  
    -   [RANK를 사용하여 검색 결과 제한](limit-search-results-with-rank.md)  
  
    -   [전체 텍스트 쿼리 성능 향상](improve-the-performance-of-full-text-queries.md)  
  
    -   [검색 속성 목록을 사용하여 문서 속성 검색](search-document-properties-with-search-property-lists.md)  
  
    -   [검색 속성의 속성 집합 GUID 및 속성 정수 ID찾기](find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
-   카탈로그 및 인덱스 관리  
  
    -   [전체 텍스트 카탈로그 만들기 및 관리](create-and-manage-full-text-catalogs.md)  
  
    -   [전체 텍스트 인덱스 만들기 및 관리](create-and-manage-full-text-indexes.md)  
  
    -   [전체 텍스트 인덱스 생성 시 언어 선택](choose-a-language-when-creating-a-full-text-index.md)  
  
    -   [전체 텍스트 인덱스 채우기](populate-full-text-indexes.md)  
  
    -   [전체 텍스트 인덱스 관리](../../database-engine/manage-full-text-indexes.md)  
  
    -   [전체 텍스트 인덱스 성능 향상](improve-the-performance-of-full-text-indexes.md)  
  
    -   [전체 텍스트 인덱싱 문제 해결](troubleshoot-full-text-indexing.md)  
  
    -   [전체 텍스트 카탈로그와 인덱스 백업 및 복원](back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   언어 구성 요소 관리  
  
    -   [검색 필터 구성 및 관리](configure-and-manage-filters-for-search.md)  
  
    -   [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
    -   [등록된 필터와 단어 분리기 보기 및 변경](view-or-change-registered-filters-and-word-breakers.md)  
  
    -   [검색에 사용된 단어 분리기를 이전 버전으로 되돌리기](revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
    -   [미국 영어 및 영국 영어에 사용되는 단어 분리기 변경](change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
    -   [사용자 지정 사전을 사용하여 단어 분리기의 동작 사용자 지정](customize-the-behavior-of-word-breakers-with-a-custom-dictionary.md)  
  
    -   [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
    -   [전체 텍스트 검색에 사용할 동의어 사전 파일 구성 및 관리](configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
-   전체 텍스트 검색 관리  
  
    -   [서버 인스턴스의 전체 텍스트 검색 관리 및 모니터링](manage-and-monitor-full-text-search-for-a-server-instance.md)  
  
    -   [전체 텍스트 필터 데몬 시작 관리자 서비스 계정 설정](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
  
-   [전체 텍스트 검색 업그레이드](upgrade-full-text-search.md)  
  
 [항목 내용](#top)  
  
##  <a name="relcontent"></a> 관련 내용  
  
-   [전체 텍스트 검색 DDL, 함수, 저장 프로시저 및 뷰](../views/views.md)  
  
 [항목 내용](#top)  
  
  
