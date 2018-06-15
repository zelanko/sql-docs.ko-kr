---
title: SQL Server 에이전트 오류 로그 재활용 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e1845c8b775debcd15a195826ec4a2912fbf1bd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33040800"
---
# <a name="recycle-sql-server-agent-error-logs"></a>SQL Server 에이전트 오류 로그 재활용
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 오류 로그를 재활용할 수 있습니다. 이 로그를 재활용하면 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 오류 로그가 닫히고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 다시 시작되지 않은 상태에서 새 오류 로그가 시작됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트는 최근 9개의 오류 로그를 유지 관리합니다. 오류 로그가 9개 있는 경우에 오류 로그를 재활용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 가장 오래된 오류 로그가 제거됩니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 에이전트 오류 로그](../../ssms/agent/sql-server-agent-error-log.md)  
  
