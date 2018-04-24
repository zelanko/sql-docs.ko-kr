---
title: SQL Server 에이전트 오류 로그 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 183d3d165ae1b32a18707b117fa2e2ce6faf729c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-agent-error-log"></a>SQL Server 에이전트 오류 로그
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트는 기본적으로 경고 및 오류를 기록하는 오류 로그를 만듭니다. 이 로그에는 다음 경고 및 오류가 표시됩니다.  
  
-   "\<*job_name*> 작업이 실행 중에 삭제되었습니다."와 같은 잠재적 문제에 대한 정보를 제공하는 경고 메시지  
  
-   "메일 세션을 시작할 수 없습니다"와 같이 대개 시스템 관리자의 조정이 필요한 오류 메시지. 오류 메시지는 **net send**로 특정 사용자나 컴퓨터에 전달될 수 있습니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 오류 로그를 최대 9개까지 유지 관리합니다. 보관된 오류 로그에는 각각 오류 로그의 상대적 기간을 표시하는 확장명이 있습니다. 예를 들어 .1의 확장명은 최근에 보관된 오류 로그를 표시하고 .9의 확장명은 가장 오래된 오류 로그를 표시합니다.  
  
기본적으로 실행 추적 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 오류 로그를 가득 채울 수 있으므로 이 로그에 기록되지 않습니다. 오류 로그가 가득 차게 되면 좀 더 중요한 오류를 놓칠 수 있는 가능성이 높아집니다. 오류 로그는 서버의 처리 부하에도 영향을 주기 때문에 실행 추적 메시지를 오류 로그로 캡처할 경우 얻을 수 있는 가치에 대해 신중하게 고려해야 합니다. 일반적으로 특정 문제를 디버깅할 때만 모든 메시지를 캡처하는 것이 가장 좋습니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 중지되었을 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 오류 로그의 위치를 수정할 수 있습니다. 오류 로그가 비어 있으면 로그를 열 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트를 중단하지 않고 언제든지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 로그를 반복할 수 있습니다.  
  
**SQL Server 에이전트 오류 로그를 보려면**  
  
-   [SQL Server 에이전트 오류 로그 보기&#40;SQL Server Management Studio&#41;](../../ssms/agent/view-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**SQL Server 에이전트 오류 로그 이름을 바꾸려면**  
  
-   [SQL Server 에이전트 오류 로그 이름 바꾸기&#40;SQL Server Management Studio&#41;](../../ssms/agent/rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**SQL Server 에이전트 오류 메시지를 보내려면**  
  
-   [Send SQL Server Agent Error Messages](../../ssms/agent/send-sql-server-agent-error-messages.md)  
  
**실행 추적 메시지를 SQL Server 에이전트 오류 로그에 쓰려면**  
  
-   [SQL Server 에이전트 오류 로그에 실행 추적 메시지 작성&#40;SQL Server Management Studio&#41;](../../ssms/agent/write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
