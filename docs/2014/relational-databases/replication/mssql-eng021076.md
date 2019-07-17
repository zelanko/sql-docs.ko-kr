---
title: MSSQL_ENG021076 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021076 error
ms.assetid: 612e5c59-ba3e-49c3-a3df-56bac3d850a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23bd163d63fa3939e35facc49cb3be7f8f07ff91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023211"
---
# <a name="mssqleng021076"></a>MSSQL_ENG021076
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21076|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|아티클 '%s'의 초기 스냅샷을 아직 사용할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 스냅샷 에이전트에서 스냅샷 생성을 완료하기 전에 배포 에이전트가 시작되는 경우 MSSQL_ENG021076 오류가 발생할 수 있습니다. 이 오류는 게시에 아티클이 하나만 있을 때 발생합니다. 게시에 두 개 이상의 아티클이 있으면 MSSQL_ENG021075 오류가 발생합니다. 자세한 내용은 [MSSQL_ENG021075](mssql-eng021075.md)을(를) 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
 구독이 생성된 후 게시의 스냅샷 에이전트가 시작되지 않은 경우 또는 구독을 다시 초기화하도록 마지막으로 선택한 후 스냅샷 에이전트가 시작되지 않은 경우 배포 에이전트를 시작하기 전에 스냅샷 에이전트를 시작한 다음 완료해야 합니다. 자세한 내용은 [스냅샷 만들기 및 적용](create-and-apply-the-snapshot.md)을 참조하세요.  
  
 스냅샷 에이전트가 완료되지 않는 경우 스냅샷 에이전트 기록에서 오류를 확인한 후 해결합니다. 복제 모니터에서 에이전트 상태 및 오류 정보를 보는 방법에 대한 자세한 내용은 [복제 모니터를 사용하여 정보 보기 및 작업 수행](monitor/view-information-and-perform-tasks-replication-monitor.md)을 참조하세요.  
  
 오류가 계속 발생하면 에이전트의 로깅을 늘리고 해당 로그의 출력 파일을 지정하십시오. 오류의 컨텍스트에 따라 이러한 작업을 수행하면 오류 및/또는 추가 오류 메시지가 발생할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
