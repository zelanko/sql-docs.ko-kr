---
title: "SQL Server 에이전트 속성(기록 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 51839ab3d459e2350c582810fe003fc5086de3eb
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-agent-properties-history-page"></a>SQL Server 에이전트 속성(기록 페이지)
이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 기록 로그 관리에 대한 설정을 확인하고 수정할 수 있습니다.  
  
## <a name="options"></a>옵션  
**작업 기록 로그 크기 제한**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 로그에 보존할 작업 기록 정보의 크기 제한을 설정합니다.  
  
**작업 기록 로그의 최대 크기(행 수)**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 보존할 최대 행 수를 설정합니다. 로그의 행 수가 이 수에 도달한 경우 새 행을 입력하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 가장 오래된 행을 제거합니다.  
  
**작업당 작업 기록의 최대 행 수**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 작업당 보존할 최대 행 수를 설정합니다. 특정 작업 기록의 행 수가 이 수에 도달한 경우 새 행을 입력하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 로그에서 가장 오래된 행을 제거합니다.  
  
**에이전트 기록 제거**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 지정된 기간보다 오래된 항목을 로그에서 제거하도록 지정합니다. 이 작업은 기록을 제거하는 일회 실행 작업입니다. 작업을 되풀이해야 하는 경우에는 정리 작업을 사용하여 유지 관리 계획을 만들고 예약하십시오.  
  
**다음보다 오래된 항목**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 항목을 보존하는 기간을 설정합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 에이전트 오류 로그](../../ssms/agent/sql-server-agent-error-log.md)  
  

