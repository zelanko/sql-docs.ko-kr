---
title: MSSQLSERVER_18264 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 18264 (Database Engine error)
ms.assetid: 3050fc56-2be5-43cf-916b-50a3ac5f89aa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2445b0c62347d84beb4690541871bfdec8d1ca3a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62869568"
---
# <a name="mssqlserver_18264"></a>MSSQLSERVER_18264
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|Microsoft SQL Server|  
|이벤트 ID|18264|  
|이벤트 원본|MSSQLENGINE|  
|구성 요소|SQLEngine|  
|심볼 이름|STRMIO_DBDUMP|  
|메시지 텍스트|데이터베이스가 백업되었습니다. 데이터베이스: %s, 만든 날짜(시간): %s(%s), 덤프한 페이지 수: %d, 첫 번째 LSN: %s, 마지막 LSN: %s, 덤프 디바이스 수: %d, 디바이스 정보: (%s). 이 메시지는 정보 제공용이므로 추가적인 조치가 필요하지 않습니다.|  
  
## <a name="explanation"></a>설명  
 기본적으로 백업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 이 정보 메시지가 추가됩니다. 트랜잭션 로그를 자주 백업하는 경우 이러한 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 추적 플래그 **3226**을 사용하여 이러한 로그 항목을 표시하지 않을 수 있습니다. 로그 백업을 자주 실행하거나 이러한 항목에 종속되는 스크립트가 없는 경우 이 추적 플래그를 설정하면 유용합니다.  
  
 추적 플래그를 사용하는 방법은 SQL Server 온라인 설명서를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [추적 플래그&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)  
  
  
