---
title: 작업 만들기 | Microsoft 문서
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
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: 465fb7fc-7622-4252-a178-ea51691c935b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bff559fe6994a55e6ab7f9da651057209a5c5355
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42774445"
---
# <a name="create-jobs"></a>작업 만들기
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

작업이란 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 순차적으로 수행하는 일련의 지정된 작업입니다. 작업은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트, 명령 프롬프트 응용 프로그램, Microsoft ActiveX 스크립트, Integration Services 패키지, Analysis Services 명령 및 쿼리 또는 복제 태스크를 실행하는 등 광범위한 활동을 수행합니다. 작업은 반복적인 태스크나 예약 가능한 태스크를 실행하고 경고를 발생시켜 작업 상태를 사용자에게 자동으로 알리므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리를 매우 단순하게 만들어 줍니다.  
  
작업을 만들려면 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할이나 **sysadmin** 고정 서버 역할 중 하나의 멤버여야 합니다. 작업은 소유자나 **sysadmin** 역할의 멤버만 편집할 수 있습니다. **sysadmin** 역할의 멤버는 작업 소유권을 다른 사용자에게 할당할 수 있으며 작업 소유자가 아니어도 모든 작업을 실행할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
작업은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 로컬 인스턴스나 엔터프라이즈 내의 다중 인스턴스에서 실행되도록 작성할 수 있습니다. 다중 서버에서 작업을 실행하려면 적어도 마스터 서버 한 대와 대상 서버 한 대 이상을 설정해야 합니다. 마스터 및 대상 서버에 대한 자세한 내용은 [기업 내 관리 자동화](../../ssms/agent/automated-administration-across-an-enterprise.md)를 참조하세요.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 작업과 작업 단계 정보를 작업 기록에 기록합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**설명**|**항목**|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만드는 방법에 대해 설명합니다.|[작업 만들기](../../ssms/agent/create-a-job.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업의 소유권을 다른 사용자에게 다시 할당하는 방법에 대해 설명합니다.|[Give Others Ownership of a Job](../../ssms/agent/give-others-ownership-of-a-job.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 기록 로그를 설정하는 방법에 대해 설명합니다.|[Set Up the Job History Log](../../ssms/agent/set-up-the-job-history-log.md)|  
  
## <a name="see-also"></a>참고 항목  
[작업 단계 관리](../../ssms/agent/manage-job-steps.md)  
[기업 내 관리 자동화](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[일정을 만들고 작업에 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[작업 실행](../../ssms/agent/run-jobs.md)  
[작업 보기 또는 수정](../../ssms/agent/view-or-modify-jobs.md)  
  
