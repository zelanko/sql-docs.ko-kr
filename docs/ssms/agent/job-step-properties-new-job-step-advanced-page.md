---
title: 작업 단계 속성 - 새 작업 단계(고급 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.stepadvanced.f1
ms.assetid: bdecfd4f-bcd8-4ba2-8ada-fbb636314f40
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f18312b685adc310af69473966f70ed81202390e
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095792"
---
# <a name="job-step-properties---new-job-step-advanced-page"></a>작업 단계 속성 - 새 작업 단계(고급 페이지)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계의 속성을 확인하고 변경할 수 있습니다.  
  
## <a name="options"></a>옵션  
**성공한 경우 동작**  
작업 단계 성공 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 수행할 동작을 설정합니다.  
  
**다시 시도 횟수**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 실패한 작업 단계를 다시 시도하는 횟수를 설정합니다.  
  
**다시 시도 간격(분)**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 작업 단계를 다시 시도하기 전에 대기하는 시간을 설정합니다.  
  
**실패한 경우 동작**  
작업 단계 실패 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 수행할 동작을 설정합니다.  
  
## <a name="options-for-transact-sql-job-steps"></a>Transact-SQL 작업 단계 옵션  
**출력 파일**  
작업 단계의 출력에 사용할 파일을 설정합니다. 이 옵션은 **sysadmin** 고정 서버 역할의 멤버만 사용할 수 있습니다.  
  
**...**  
작업 단계의 출력에 사용할 파일을 찾아 봅니다.  
  
**보기**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 이 단추를 사용하여 출력 파일을 표시할 수 없습니다. 대신 메모장을 사용하여 작업 단계 출력 파일을 검토합니다.  
  
**기존 파일에 출력 추가**  
출력을 파일의 기존 내용에 추가합니다. 그렇지 않으면 작업 단계가 실행될 때마다 이전 파일 내용을 덮어씁니다.  
  
**테이블에 기록**  
작업 단계 출력을 **msdb** 데이터베이스의 **sysjobstepslogs** 테이블에 기록합니다.  
  
**보기**  
작업 단계가 최소 한 번 실행된 후에는 **보기** 를 클릭하여 테이블에 기록된 출력을 볼 수 있습니다.  
  
**테이블의 기존 항목에 출력 추가**  
테이블의 기존 내용에 출력을 추가합니다. 그렇지 않으면 작업 단계가 실행될 때마다 이전 테이블 내용을 덮어씁니다.  
  
**기록에 단계 출력 포함**  
작업 기록에 작업 단계의 출력을 포함하려면 이 옵션을 선택합니다.  
  
**다음 사용자 이름으로 실행**  
사용자가 **sysadmin** 고정 서버 역할의 멤버인 경우 다른 SQL 로그인을 선택하여 이 작업 단계를 실행할 수 있습니다.  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>운영 체제(CmdExec) 작업 단계 옵션  
**출력 파일**  
작업 단계의 출력에 사용할 파일을 설정합니다.  
  
**...**  
작업 단계의 출력에 사용할 파일을 찾아 봅니다.  
  
**보기**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 이 단추를 사용하여 출력 파일을 표시할 수 없습니다. 대신 메모장을 사용하여 작업 단계 출력 파일을 검토합니다.  
  
**기존 파일에 출력 추가**  
작업 단계를 실행할 때마다 이전 파일 내용에 작업 단계 출력을 추가합니다.  
  
**테이블에 기록**  
작업 단계 출력을 **msdb** 데이터베이스의 **sysjobstepslogs** 테이블에 기록합니다.  
  
**보기**  
작업 단계가 최소 한 번 실행된 후에는 **보기** 를 클릭하여 테이블에 기록된 출력을 볼 수 있습니다.  
  
**테이블의 기존 항목에 출력 추가**  
테이블의 기존 내용에 출력을 추가합니다. 그렇지 않으면 작업 단계가 실행될 때마다 이전 테이블 내용을 덮어씁니다.  
  
**기록에 단계 출력 포함**  
작업 기록에 작업 단계의 출력을 포함하려면 이 옵션을 선택합니다.  
  
## <a name="options-for-powershell-job-steps"></a>PowerShell 작업 단계 옵션  
**출력 파일**  
작업 단계의 출력에 사용할 파일을 설정합니다.  
  
**...**  
작업 단계의 출력에 사용할 파일을 찾아 봅니다.  
  
**보기**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 이 단추를 사용하여 출력 파일을 표시할 수 없습니다. 대신 메모장을 사용하여 작업 단계 출력 파일을 검토합니다.  
  
**기존 파일에 출력 추가**  
작업 단계를 실행할 때마다 이전 파일 내용에 작업 단계 출력을 추가합니다.  
  
**테이블에 기록**  
작업 단계 출력을 **msdb** 데이터베이스의 **sysjobstepslogs** 테이블에 기록합니다.  
  
**보기**  
작업 단계가 최소 한 번 실행된 후에는 **보기** 를 클릭하여 테이블에 기록된 출력을 볼 수 있습니다.  
  
**테이블의 기존 항목에 출력 추가**  
테이블의 기존 내용에 출력을 추가합니다. 그렇지 않으면 작업 단계가 실행될 때마다 이전 테이블 내용을 덮어씁니다.  
  
**기록에 단계 출력 포함**  
작업 기록에 작업 단계의 출력을 포함하려면 이 옵션을 선택합니다.  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>복제 큐 판독기 작업 단계 옵션  
**Server**  
복제 큐 판독기 작업 단계에 사용할 서버를 설정합니다.  
  
**데이터베이스 백업**  
복제 큐 판독기 작업 단계에 사용할 데이터베이스를 설정합니다.  
  
## <a name="options-for-sql-server-analysis-services-job-steps"></a>SQL Server Analysis Services 작업 단계 옵션  
**출력 파일**  
작업 단계의 출력에 사용할 파일을 설정합니다. 이 옵션은 **sysadmin** 고정 서버 역할의 멤버만 사용할 수 있습니다.  
  
**...**  
작업 단계의 출력에 사용할 파일을 찾아 봅니다.  
  
**보기**  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 이 단추를 사용하여 출력 파일을 표시할 수 없습니다. 대신 메모장을 사용하여 작업 단계 출력 파일을 검토합니다.  
  
**기존 파일에 출력 추가**  
출력을 파일의 기존 내용에 추가합니다. 그렇지 않으면 작업 단계가 실행될 때마다 이전 파일 내용을 덮어씁니다.  
  
**테이블에 기록**  
작업 단계 출력을 **msdb** 데이터베이스의 **sysjobstepslogs** 테이블에 기록합니다.  
  
**보기**  
작업 단계가 최소 한 번 실행된 후에는 **보기** 를 클릭하여 테이블에 기록된 출력을 볼 수 있습니다.  
  
**테이블의 기존 항목에 출력 추가**  
테이블의 기존 내용에 출력을 추가합니다. 그렇지 않으면 작업 단계가 실행될 때마다 이전 테이블 내용을 덮어씁니다.  
  
**기록에 단계 출력 포함**  
작업 기록에 작업 단계의 출력을 포함하려면 이 옵션을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
[작업 단계 관리](../../ssms/agent/manage-job-steps.md)  
  
