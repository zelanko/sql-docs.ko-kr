---
title: "MSSQLSERVER_30089 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 9992 (Database Engine error)
ms.assetid: 188e5bde-6865-4740-a2b2-582be8f55c77
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: b20c4c44f34fc7a0a58001fd64642feda0c587bc
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver30089"></a>MSSQLSERVER_30089
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|30089|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|IFTS_FDHOST_TERMINATEDABNORMAL|  
|메시지 텍스트|전체 텍스트 필터 데몬 호스트(FDHost) 프로세스가 비정상적으로 중지되었습니다. 전체 텍스트 인덱싱 또는 쿼리 처리 작업을 수행하는 동안 단어 분리기, 형태소 분석기 또는 필터와 같은 언어 구성 요소가 잘못 구성되었거나 제대로 작동하지 않아 오류가 발생한 경우일 수 있습니다. 프로세스는 자동으로 다시 시작됩니다.|  
  
## <a name="explanation"></a>설명  
전체 텍스트 필터 데몬 호스트에서 오류가 발생하여 비정상적으로 중지되었습니다. 문제의 원인은 잘못된 형식의 문서, 필터나 단어 분리기의 버그, 필터 데몬의 문제일 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
일반적으로 데몬이 오류를 복구하지만 문제가 지속되면 이를 해결해야 합니다. 다음 방법을 사용하여 문제를 해결해 보십시오.  
  
1.  최근에 새로운 언어 구성 요소를 설치한 경우 시스템에서 이를 제거합니다.  
  
2.  탐색 로그를 보고 전체 텍스트 인덱스에 실패한 새 문서가 있는지 확인한 후 이를 제거합니다.  
  
## <a name="see-also"></a>관련 항목:  
[sp_help_fulltext_system_components&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[검색 필터 구성 및 관리](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  
