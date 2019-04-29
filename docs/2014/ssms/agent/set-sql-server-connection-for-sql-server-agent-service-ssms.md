---
title: SQL Server 에이전트 서비스 (SQL Server Management Studio)에 대 한 SQL Server 연결 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a1d02ef690dc8ce9ecca3f51d86203e306ea5589
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63034442"
---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set the SQL Server Connection for the SQL Server Agent Service (SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에이전트와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]간의 연결을 설정하는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 Windows 인증을 사용하여 SQL Server의 로컬 인스턴스에 연결할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **SQL Server 에이전트에 대한 SQL Server 연결을 설정하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   사용 권한이 있는 경우에만 개체 탐색기에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 노드가 표시됩니다.  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지원하지 않습니다. 이 옵션은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 관리할 때만 사용할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 해당 기능을 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 **sysadmin** 고정 서버 역할 멤버인 계정의 자격 증명을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트를 구성해야 합니다. 이 계정에는 다음과 같은 Windows 사용 권한이 필요합니다.  
  
-   서비스로 로그온(SeServiceLogonRight)  
  
-   프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)  
  
-   트래버스 검사 무시(SeChangeNotifyPrivilege)  
  
-   프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)  
  
 에 필요한 Windows 사용 권한에 대 한 자세한 내용은 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정 참조 [SQL Server 에이전트 서비스 계정 선택](select-an-account-for-the-sql-server-agent-service.md) 및 [Configure Windows Service Accounts 및 사용 권한](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-set-the-sql-server-connection"></a>SQL Server 연결을 설정하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 SQL Server 에이전트 서비스에 대한 연결을 사용하여 설정할 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **SQL Server 에이전트 속성** 대화 상자의 **페이지 선택**에서 **연결**을 클릭합니다.  
  
4.  **SQL Server 연결**에서 **Windows 인증 사용**을 선택하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 인스턴스에 연결할 수 있도록 합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 데이터베이스에 연결하려면 Windows 인증이 필요합니다.  
  
  
