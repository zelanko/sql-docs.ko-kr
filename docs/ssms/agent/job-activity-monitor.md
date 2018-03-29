---
title: 작업 활동 모니터 | Microsoft 문서
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
f1_keywords:
- sql13.ag.jobactivitymonitor.alljobs.f1
- SQL13.SWB.ACTIVITYMON.F1
ms.assetid: 11f2182c-5f71-46f8-8d2b-74f0fc48f2d6
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1684b3b361e7a31dbad05c9b0151a1ee25498e42
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="job-activity-monitor"></a>작업 활동 모니터
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업의 현재 활동을 볼 수 있습니다. **필터** 를 클릭하여 표시되는 작업의 수를 제한할 수 있습니다. **에이전트 작업 활동** 표는 읽기 전용입니다. 표를 정렬하려면 열 머리글을 클릭합니다. 작업을 수정하려면 작업을 두 번 클릭하여 **작업 속성** 대화 상자를 엽니다. 표에서 작업을 마우스 오른쪽 단추로 클릭하여 모든 작업 단계의 실행을 시작하거나, 특정 작업 단계에서 시작하거나, 작업을 활성화 또는 비활성화하거나, 작업을 새로 고치거나, 작업을 삭제하거나, 작업 기록이나 작업 속성을 확인하는 등의 작업을 수행할 수 있습니다. 현재 정보로 표를 업데이트하려면 **새로 고침** 을 클릭합니다.  
  
## <a name="options"></a>변수  
**이름**  
작업의 이름입니다.  
  
**Enabled**  
작업을 사용할지(**예**) 또는 사용하지 않을지(**아니요**)를 지정합니다.  
  
**상태***  
작업의 현재 상태입니다.  
  
**마지막 실행 결과**  
마지막으로 실행했을 때의 작업 상태입니다.  
  
**마지막 실행**  
서버의 로컬 날짜 및 시간을 사용하여 마지막으로 작업을 실행한 날짜 및 시간입니다.  
  
**다음 실행***  
서버의 로컬 날짜 및 시간을 사용하여 다음에 작업을 실행하기로 예약한 날짜 및 시간입니다.  
  
**범주**  
작업에 지정된 작업 범주입니다.  
  
**실행 가능**  
작업을 실행할 수 있으면**예** 이고 작업을 실행할 수 없으면 **아니요** 입니다. 단계나 대상 서버가 없는 경우 작업을 실행할 수 없습니다.  
  
**예약**  
작업이 작업 일정에 할당되어 있으면**예** 이고, 그렇지 않으면 **아니요** 입니다.  
  
* [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sysadmin 고정 서버 역할과 서버 관리자 그룹의 멤버만 이 열의 값을 볼 수 있습니다. SQLAgentOperatorRole 역할의 멤버는 이 열의 값을 볼 수 없습니다.  
  
#### <a name="to-open-the-job-activity-monitor"></a>작업 활동 모니터를 열려면  
  
-   **개체 탐색기**에서 해당 서버를 확장하고 **SQL Server 에이전트**를 확장한 다음 **작업 활동 모니터**를 마우스 오른쪽 단추로 클릭하고 **작업 활동 보기**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
[작업 활동 모니터링](../../ssms/agent/monitor-job-activity.md)  
  
