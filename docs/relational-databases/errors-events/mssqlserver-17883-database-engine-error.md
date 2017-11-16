---
title: "MSSQLSERVER_17883 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17883 (Database Engine error)
ms.assetid: adaf1c04-e397-4a69-90b8-9353a37277ea
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6228ef52269a304a5e72a3ff3bc50b915ab372f4
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17883"></a>MSSQLSERVER_17883
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17883|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SRV_SCHEDULER_NONYIELDING|  
|메시지 텍스트|프로세스 %ld:%ld:%ld(0x%lx) 작업자 0x%p이(가) 스케줄러 %ld에서 잠긴 것 같습니다. 스레드 만든 시간: %I64d. 대략적인 스레드 CPU 사용량: 커널 %I64dms, 사용자 %I64dms. 프로세스 사용률 %d%%. 시스템 유휴 시간 %d%%. 간격: %I64dms.|  
  
## <a name="explanation"></a>설명  
스케줄러에서 잠긴 스레드와 관련된 문제가 있을 수 있음을 나타냅니다.  이 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버그 때문에 발생하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 충분한 실행 주기가 없는 경우에 발생할 수 있습니다.  이 오류는 스레드가 결국 양도되면 나타나지 않을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
시스템 로드가 너무 많으면 로드를 줄이고, 그렇지 않으면 Microsoft 고객 지원 서비스에 문의합니다.  
  

