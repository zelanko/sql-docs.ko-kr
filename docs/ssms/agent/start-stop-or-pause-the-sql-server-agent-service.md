---
title: "SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, starting
- SQL Server Agent, pausing
- SQL Server Agent, stopping
ms.assetid: c95a9759-dd30-4ab6-9ab0-087bb3bfb97c
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 47bf92590470b4a318c1e25656ff74641131bfac
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="start-stop-or-pause-the-sql-server-agent-service"></a>SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 SQL Server 에이전트 서비스를 시작, 중지 또는 다시 시작하는 방법에 대해 설명합니다.  
  
운영 체제 시작 시 자동으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스가 시작되도록 구성하거나 작업을 완료해야 할 때 수동으로 시작할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 중지 또는 일시 중지하면 작업, 운영자 알림 및 경고를 일시 중지할 수 있습니다.  
  
**항목 내용**  
  
-   **시작하기 전에:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   [SQL Server Management Studio를 사용하여 SQL Server 에이전트 서비스를 시작, 중지 또는 다시 시작하려면](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전에  
  
### <a name="Restrictions"></a>제한 사항  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 실행해야 합니다. 자세한 내용은 [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)을 참조하세요.  
  
-   사용 권한이 있는 경우에만 개체 탐색기에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 노드가 표시됩니다.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
해당 기능을 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서 **sysadmin** 고정 서버 역할 멤버인 계정의 자격 증명을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에이전트를 구성해야 합니다. 이 계정에는 다음과 같은 Windows 사용 권한이 필요합니다.  
  
-   서비스로 로그온(SeServiceLogonRight)  
  
-   프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)  
  
-   트래버스 검사 무시(SeChangeNotifyPrivilege)  
  
-   프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 계정에 필요한 Windows 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 서비스의 계정 선택](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) 및 [Windows 서비스 계정 설정](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014)을 참조하세요.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-start-stop-or-restart-the-sql-server-agent-service"></a>SQL Server 에이전트 서비스를 시작, 중지 또는 다시 시작하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 SQL Server 에이전트 서비스를 관리할 서버를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **시작**, **중지**또는 **다시 시작**을 선택합니다.  
  
3.  **사용자 계정 컨트롤** 대화 상자에서 **예**를 클릭합니다.  
  
4.  작업을 수행할지 묻는 메시지가 표시되면 **예**를 클릭합니다.  
  
참조 항목:  
  
-   [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](http://msdn.microsoft.com/en-us/32660a02-e5a1-411a-9e57-7066ca459df6)  
  
-   [SQL Server 에이전트 자동 시작&#40;SQL Server Management Studio&#41;](../../ssms/agent/autostart-sql-server-agent-sql-server-management-studio.md)  
  
