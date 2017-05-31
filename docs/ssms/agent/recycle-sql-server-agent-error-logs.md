---
title: "SQL Server 에이전트 오류 로그 재활용 | Microsoft 문서"
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
- sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6b3b79686cbc194eda76fd1f4873d81c26d8d31c
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="recycle-sql-server-agent-error-logs"></a>SQL Server 에이전트 오류 로그 재활용
이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 오류 로그를 재활용할 수 있습니다. 이 로그를 재활용하면 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 오류 로그가 닫히고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 다시 시작되지 않은 상태에서 새 오류 로그가 시작됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트는 최근 9개의 오류 로그를 유지 관리합니다. 오류 로그가 9개 있는 경우에 오류 로그를 재활용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 가장 오래된 오류 로그가 제거됩니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 에이전트 오류 로그](../../ssms/agent/sql-server-agent-error-log.md)  
  

