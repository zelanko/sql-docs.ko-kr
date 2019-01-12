---
title: SQL Server 에이전트 오류 로그 (SQL Server Management Studio)에 실행 추적 메시지 작성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- writing trace messages
- traces [SQL Server], SQL Server Agent logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: 90e3731e-6fae-43db-833e-9accecdd1c03
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd21f4b08bf53d4715f2b99eefed523f3853c033
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100688"
---
# <a name="write-execution-trace-messages-to-the-sql-server-agent-error-log-sql-server-management-studio"></a>Write Execution Trace Messages to the SQL Server Agent Error Log (SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 해당 오류 로그에 실행 추적 메시지를 포함하도록 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   [SQL Server Management Studio를 사용 하 여 SQL Server 에이전트 오류 로그에 실행 추적 메시지를 작성 하려면](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   사용 권한이 있는 경우에만 개체 탐색기에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 노드가 표시됩니다.  
  
-   이 옵션으로 오류 로그가 더욱 커질 수 있으므로 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 문제를 조사할 때만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그에 실행 추적 메시지를 포함하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 해당 기능을 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 **sysadmin** 고정 서버 역할 멤버인 계정의 자격 증명을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트를 구성해야 합니다. 이 계정에는 다음과 같은 Windows 사용 권한이 필요합니다.  
  
-   서비스로 로그온(SeServiceLogonRight)  
  
-   프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)  
  
-   트래버스 검사 무시(SeChangeNotifyPrivilege)  
  
-   프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)  
  
 에 필요한 Windows 사용 권한에 대 한 자세한 내용은 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정 참조 [SQL Server 에이전트 서비스 계정 선택](select-an-account-for-the-sql-server-agent-service.md) 및 [Configure Windows Service Accounts 및 사용 권한](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)합니다.  
  
##  <a name="SSMSProcedure"></a>   
#### <a name="to-write-execution-trace-messages-to-the-sql-server-agent-error-log"></a>실행 추적 메시지를 SQL Server 에이전트 오류 로그에 쓰려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 실행 추적 메시지를 기록하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그가 포함된 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  에 **SQL Server 에이전트 속성-**_server_name_ 대화 상자의 **오류 로그** 에 **일반** 페이지에서 선택 합니다 **실행 추적 메시지 포함** 확인란 합니다.  
  
4.  **확인**을 클릭합니다.  
  
  
