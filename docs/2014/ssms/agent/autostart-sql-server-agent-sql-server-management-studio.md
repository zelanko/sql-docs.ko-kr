---
title: SQL Server 에이전트 자동 시작(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, starting
- autostart SQL Server Agent
ms.assetid: 2ea332da-0ede-4d2b-b122-c4c10eaca191
author: stevestein
ms.author: sstein
ms.openlocfilehash: ef904e7f8a6011155a0c1aad21af3d6a4d84d847
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011766"
---
# <a name="autostart-sql-server-agent-sql-server-management-studio"></a>Autostart SQL Server Agent (SQL Server Management Studio)
  이 항목 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는에서 예기치 않게 중지 되어야 하는 경우 자동으로 다시 시작 되도록 에이전트를 구성 하는 방법에 대해 설명 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   [SQL Server Management Studio를 사용하여 자동으로 시작되도록 SQL Server 에이전트를 구성하려면](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 사용 권한이 있는 경우에만 개체 탐색기에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 노드가 표시됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 해당 기능을 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 **sysadmin** 고정 서버 역할 멤버인 계정의 자격 증명을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트를 구성해야 합니다. 이 계정에는 다음과 같은 Windows 사용 권한이 필요합니다.  
  
-   서비스로 로그온(SeServiceLogonRight)  
  
-   프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)  
  
-   트래버스 검사 무시(SeChangeNotifyPrivilege)  
  
-   프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)  
  
 에이전트 서비스 계정에 필요한 Windows 사용 권한에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 에이전트 서비스에 대 한 계정 선택](select-an-account-for-the-sql-server-agent-service.md) 및 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조 하세요.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-sql-server-agent-to-automatically-restart"></a>자동으로 다시 시작되도록 SQL Server 에이전트를 구성하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 자동으로 다시 시작되도록 SQL Server 에이전트를 구성할 서버를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **일반** 페이지에서 **SQL Server 에이전트가 갑자기 작동을 멈추면 자동으로 다시 시작**을 선택합니다.  
  
  
