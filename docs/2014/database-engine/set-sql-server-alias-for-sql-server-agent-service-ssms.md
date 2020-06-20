---
title: SQL Server 에이전트 서비스 (SQL Server Management Studio)의 SQL Server 별칭을 설정 합니다. Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b9f91ec957665975fd956e36a5af3c4261fb47af
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929194"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
  이 항목에서는를 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용 하 여 에이전트에서에 연결 하는 데 사용할 별칭 [!INCLUDE[ssDE](../includes/ssde-md.md)] 을 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 설정 하는 방법에 대해 설명 합니다. 기본적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 서비스는 추가 클라이언트 구성이 필요 없는 동적 서버 이름을 사용하여 명명된 파이프에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 인스턴스에 연결합니다. 기본 네트워크 전송을 사용하지 않는 경우나 다른 명명된 파이프에서 수신하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 인스턴스에 연결 중인 경우에만 서버 연결 별칭을 구성해야 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   [SQL Server Management Studio를 사용하여 SQL Server 에이전트 서비스에 대한 SQL Server 별칭을 설정하려면](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 로컬 인스턴스를 참조하는 별칭을 선택하지 않으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에이전트가 제대로 작동하지 않습니다.  
  
-   사용 권한이 있는 경우에만 개체 탐색기에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 노드가 표시됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 해당 기능을 수행하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 **sysadmin** 고정 서버 역할 멤버인 계정의 자격 증명을 사용하도록 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에이전트를 구성해야 합니다. 이 계정에는 다음과 같은 Windows 사용 권한이 필요합니다.  
  
-   서비스로 로그온(SeServiceLogonRight)  
  
-   프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)  
  
-   트래버스 검사 무시(SeChangeNotifyPrivilege)  
  
-   프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)  
  
 에이전트 서비스 계정에 필요한 Windows 사용 권한에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [SQL Server 에이전트 서비스에 대 한 계정 선택](../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) 및 [Windows 서비스 계정 및 권한 구성](configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조 하세요.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>SQL Server 에이전트 서비스에 대한 SQL Server 별칭을 설정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **SQL Server 에이전트 속성**_server_name_ 대화 상자의 **페이지 선택**에서 **연결**을 선택 하 고  
  
4.  **로컬 호스트 서버 별칭** 상자에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트에서 연결할 서버의 별칭을 입력합니다.  
  
5.  **확인**을 클릭합니다.  
  
  
