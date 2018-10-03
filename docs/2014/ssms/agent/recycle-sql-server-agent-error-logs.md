---
title: SQL Server 에이전트 오류 로그 재활용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72c3b0ee6af23f38871cc319e700c1680b5e134f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074983"
---
# <a name="recycle-sql-server-agent-error-logs"></a>SQL Server 에이전트 오류 로그 재활용
  이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그를 재활용할 수 있습니다. 이 로그를 재활용하면 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그가 닫히고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 다시 시작되지 않은 상태에서 새 오류 로그가 시작됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 최근 9개의 오류 로그를 유지 관리합니다. 오류 로그가 9개 있는 경우에 오류 로그를 재활용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 가장 오래된 오류 로그가 제거됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 오류 로그](sql-server-agent-error-log.md)  
  
  
