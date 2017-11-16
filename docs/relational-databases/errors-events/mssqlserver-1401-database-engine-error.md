---
title: "MSSQLSERVER_1401 | Microsoft 문서"
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
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1968d85a421b61fa31dbe2a83c7f7773c8a89db0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1401|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBM_MASTERSTARTUP|  
|메시지 텍스트|다음과 같은 이유로 인해 데이터베이스 미러링 마스터 스레드 루틴을 시작하지 못했습니다: %ls. 이 오류의 원인을 수정한 다음 SQL Server 서비스를 다시 시작하십시오.|  
  
## <a name="explanation"></a>설명  
미러링 제어 스레드를 시작하지 못했습니다.  
  
## <a name="user-action"></a>사용자 동작  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에서 이 메시지 이전에 발생한 관련 오류를 찾으십시오. 이 오류의 원인을 수정한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스(MSSQLSERVER)를 다시 시작하세요.  
  
## <a name="see-also"></a>관련 항목:  
[데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  

