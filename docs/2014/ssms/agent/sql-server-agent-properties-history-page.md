---
title: SQL Server 에이전트 속성(기록 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 46a62984a55b5141f66fb459b42274fe3ca94c1d
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818189"
---
# <a name="sql-server-agent-properties-history-page"></a>SQL Server 에이전트 속성(기록 페이지)
  이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 기록 로그 관리에 대한 설정을 확인하고 수정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **작업 기록 로그 크기 제한**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 로그에 보존할 작업 기록 정보의 크기 제한을 설정합니다.  
  
 **작업 기록 로그의 최대 크기(행 수)**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 보존할 최대 행 수를 설정합니다. 로그의 행 수가 이 수에 도달한 경우 새 행을 입력하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 가장 오래된 행을 제거합니다.  
  
 **작업당 작업 기록의 최대 행 수**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 작업당 보존할 최대 행 수를 설정합니다. 특정 작업 기록의 행 수가 이 수에 도달한 경우 새 행을 입력하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 로그에서 가장 오래된 행을 제거합니다.  
  
 **에이전트 기록 제거**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 지정된 기간보다 오래된 항목을 로그에서 제거하도록 지정합니다. 이 작업은 기록을 제거하는 일회 실행 작업입니다. 작업을 되풀이해야 하는 경우에는 정리 작업을 사용하여 유지 관리 계획을 만들고 예약하십시오.  
  
 **다음보다 오래된 항목**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 항목을 보존하는 기간을 설정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 오류 로그](sql-server-agent-error-log.md)  
  
  
