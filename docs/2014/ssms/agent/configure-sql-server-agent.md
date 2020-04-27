---
title: SQL Server 에이전트 구성 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, configuring
- accounts [SQL Server], SQL Server Agent
- SQL Server Agent, permissions
- security [SQL Server], SQL Server Agent
ms.assetid: 2e361a62-9e92-4fcd-80d7-d6960f127900
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e7c8cb2230a7b6923514f0928b844f72c216d58
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63253565"
---
# <a name="configure-sql-server-agent"></a>Configure SQL Server Agent
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트의 일부 구성 옵션을 지정하는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 구성 옵션의 전체 집합은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], SMO( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 개체) 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 저장 프로시저 내에서만 사용할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   [SQL Server 에이전트를 구성하려면](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   **개체 탐색기에서** SQL Server 에이전트 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 클릭하여 작업, 연산자, 경고 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 관리합니다. 그러나 사용 권한이 있는 경우에만 개체 탐색기에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 노드가 표시됩니다.  
  
-   장애 조치(Failover) 클러스터 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 자동 다시 시작을 사용하도록 설정하면 안 됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 해당 기능을 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 **sysadmin** 고정 서버 역할 멤버인 계정의 자격 증명을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트를 구성해야 합니다. 이 계정에는 다음과 같은 Windows 사용 권한이 필요합니다.  
  
-   서비스로 로그온(SeServiceLogonRight)  
  
-   프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)  
  
-   트래버스 검사 무시(SeChangeNotifyPrivilege)  
  
-   프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정에 필요한 windows 사용 권한에 대 한 자세한 내용은 [SQL Server 에이전트 서비스에 대 한 계정 선택](select-an-account-for-the-sql-server-agent-service.md) 및 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조 하세요.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-sql-server-agent"></a>SQL Server 에이전트를 구성하려면  
  
1.  **시작** 단추를 클릭한 다음 **시작**  메뉴에서 **제어판**을 클릭합니다.  
  
2.  제어판에서 **시스템 및 보안**, **관리 도구**를 차례로 클릭한 다음 **로컬 보안 정책**을 선택합니다.  
  
3.  로컬 보안 정책에서 펼침 단추를 클릭하여 **로컬 정책** 폴더를 확장하고 **사용자 권한 할당** 폴더를 클릭합니다.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 함께 사용하도록 구성할 사용 권한을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
5.  사용 권한의 속성 대화 상자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행되는 계정이 나열되는지 확인합니다. 나열되지 않으면 **사용자 또는 그룹 추가**를 클릭하고 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행되는 계정을 입력한 다음 **확인**을 클릭합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트와 함께 실행하기 위해 추가할 각 사용 권한에 대해 이 작업을 반복합니다. 작업을 완료한 후 **확인**을 클릭합니다.  
  
  
