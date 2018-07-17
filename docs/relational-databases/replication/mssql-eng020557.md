---
title: MSSQL_ENG020557 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020557 error
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8ee2f4fbbb062ba21c585ea3aa1ccc4dc2278b4
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37355475"
---
# <a name="mssqleng020557"></a>MSSQL_ENG020557
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|20557|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|에이전트를 종료합니다. 자세한 내용은 작업 '%s'에 대한 SQL Server 에이전트 작업 기록을 참조하십시오.|  
  
## <a name="explanation"></a>설명  
 복제 에이전트가 해당 기록 테이블에 원인을 기록하지 않고 종료되었거나 에이전트가 프로세스 중에 종료되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
  
-   에이전트를 다시 시작하여 이제 오류 없이 실행되는지 확인합니다. 자세한 내용은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
-   에이전트 기록과 작업 기록에서 같은 시간대에 발생한 다른 오류를 확인합니다. 복제 모니터에서 에이전트 상태 및 오류 정보를 보는 방법은 다음 항목을 참조하십시오.  
  
    -   스냅숏 에이전트, 로그 판독기 에이전트 및 큐 판독기 에이전트에 대해서는 [게시 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)을 참조하세요.  
  
    -   배포 에이전트 및 병합 에이전트에 대해서는 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)을 참조하세요.  
  
-   에이전트에서 액세스하는 컴퓨터 사이에 기본 연결이 제대로 작동하는지 확인한 다음 **sqlcmd** 와 같은 유틸리티를 사용하여 각 컴퓨터에 연결합니다. 각 컴퓨터에 연결할 때는 에이전트 연결 시 사용하는 계정과 같은 계정을 사용합니다. 각 에이전트 계정에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
-   스냅숏을 만들거나 적용하는 동안 오류가 발생하면 스냅숏 디렉터리의 파일에서 오류를 확인합니다.  
  
-   오류가 계속 발생하면 에이전트의 로깅을 늘리고 해당 로그의 출력 파일을 지정하십시오. 오류의 컨텍스트에 따라 이러한 작업을 수행하면 오류 및 추가 오류 메시지가 발생할 수 있습니다. 복제에 대한 로깅을 구성하는 방법은 Microsoft 기술 자료 문서 [312292](http://support.microsoft.com/kb/312292)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
