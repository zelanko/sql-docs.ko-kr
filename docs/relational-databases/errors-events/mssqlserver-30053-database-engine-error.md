---
title: MSSQLSERVER_30053 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 8ad23889-e243-4bd7-bc3e-150403399d89
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d7f14aed745e4421a6ea43746d1286712834a47d
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323344"
---
# <a name="mssqlserver30053"></a>MSSQLSERVER_30053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|30053|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|메시지 텍스트|전체 텍스트 쿼리 문자열의 단어 분리 작업이 시간을 초과했습니다. 단어 분리기에서 전체 텍스트 쿼리 문자열을 처리하는 데 오랜 시간이 걸리거나 서버에서 많은 쿼리가 실행되는 경우 이 오류가 발생할 수 있습니다. 부하를 줄여 쿼리를 다시 실행하십시오.|  
  
## <a name="explanation"></a>설명  
다음과 같은 경우 단어 분리 시간 초과 오류가 발생할 수 있습니다.  
  
-   쿼리 언어용 단어 분리기가 올바르지 않게 구성된 경우. 해당 레지스트리 설정이 올바르지 않은 경우가 이에 해당합니다.  
  
-   특정 쿼리 문자열에 대해 단어 분리기가 제대로 작동하지 않는 경우  
  
-   특정 쿼리 문자열에 대해 단어 분리기가 너무 많은 데이터를 반환하는 경우 데이터가 지나치게 많으면 버퍼 오버런 공격으로 간주되어 단어 분리 서비스를 호스팅하는 필터 데몬 프로세스(fdhost.exe)가 종료될 수 있습니다.  
  
-   필터 데몬 프로세스 구성이 올바르지 않은 경우  
  
    가장 일반적인 구성 문제는 암호 만료나 필터 데몬 계정이 로그온하지 못하도록 하는 도메인 정책입니다.  
  
-   서버 인스턴스에서 실행되는 쿼리 작업의 양이 너무 많은 경우. 단어 분리기에서 전체 텍스트 쿼리 문자열을 처리하는 데 오랜 시간이 걸리거나 서버에서 많은 쿼리가 실행되는 경우가 이에 해당됩니다. 이는 가능성이 가장 낮은 원인입니다.  
  
## <a name="user-action"></a>사용자 동작  
다음과 같이 시간 초과 문제의 가능한 원인에 적합한 사용자 동작을 선택합니다.  
  
|예상 원인|사용자 동작|  
|------------------|---------------|  
|쿼리 언어용 단어 분리기가 올바르지 않게 구성된 경우|타사 단어 분리기를 사용할 경우 운영 체제에 올바르지 않게 등록되어 있을 수 있습니다. 이 경우 단어 분리기를 다시 등록하십시오. 자세한 내용은 [검색에 사용된 단어 분리기를 이전 버전으로 되돌리기](~/relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)를 참조하세요.|  
|특정 쿼리 문자열에 대해 단어 분리기가 제대로 작동하지 않는 경우|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 단어 분리기의 경우 Microsoft 고객 서비스 지원 센터에 문의하십시오.|  
|특정 쿼리 문자열에 대해 단어 분리기가 너무 많은 데이터를 반환하는 경우|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 단어 분리기의 경우 Microsoft 고객 서비스 지원 센터에 문의하십시오.|  
|필터 데몬 프로세스 구성이 올바르지 않은 경우|현재 암호를 사용 중이고 도메인 정책에서 필터 데몬 계정 로그온을 차단하고 있는지 확인하십시오.|  
|서버에서 실행되는 쿼리 작업의 양이 너무 많은 경우|부하를 줄여 쿼리를 다시 실행하십시오.|  
  
## <a name="see-also"></a>참고 항목  
[전체 텍스트 필터 데몬 시작 관리자 서비스 계정 설정](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[전체 텍스트 검색](~/relational-databases/search/full-text-search.md)  
[sp_help_fulltext_system_components&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[검색 필터 구성 및 관리](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  
