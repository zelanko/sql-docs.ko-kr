---
title: "작업 실행 종료 설정(SQL Server Management Studio) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: df7d516501546d36ac3fac900d694e1e32e2f336
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>Set Job Execution Shutdown (SQL Server Management Studio)
이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 자체적으로 종료하기 전에 실행 중인 작업을 종료하기 위해 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 대기하는 시간을 설정하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전에:**  
  
    [보안](#Security)  
  
-   **다음을 사용하여 SQL Server 에이전트 작업의 종료 시간을 설정합니다.**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전에  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
기본적으로 **sysadmin** 고정 서버 역할의 멤버는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 기다리는 시간을 설정할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-set-job-execution-shutdown"></a>작업 실행 종료를 설정하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 작업 실행 종료 간격을 설정하려는 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **페이지 선택**아래에서 **작업 시스템**을 선택합니다.  
  
4.  **시스템 종료 제한 시간 간격** 을 설정하여 시스템 종료 제한 시간 간격을 늘리거나 줄입니다. 이 값에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 자체적으로 종료하기 전에 실행 중인 작업을 종료하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 대기하는 시간이 결정됩니다.  
  

