---
title: SQL Server 에이전트의 서비스 시작 계정 설정 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, service accounts
- startup accounts [SQL Server]
- service startup accounts [SQL Server Agent]
ms.assetid: 46ffe818-ebb5-43a0-840b-923f219a2472
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a1b447afcdbded20a4ed0801922770b6338f646c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="set-the-service-startup-account-for-sql-server-agent-sql-server-configuration-manager"></a>Set the Service Startup Account for SQL Server Agent (SQL Server Configuration Manager)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 시작 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 실행되는 Windows 계정과 해당 네트워크 권한을 정의합니다. 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 구성 관리자를 통해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]에이전트 서비스 계정을 설정하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   [SQL Server Management Studio를 사용하여 SQL Server 에이전트에 대해 서비스 시작 계정을 설정하려면](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]부터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 시작 계정이 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Administrators 그룹의 멤버가 아니어도 됩니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 시작 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]sysadmin 고정 서버 역할의 멤버여야 합니다. 다중 서버 작업 처리를 사용하려면 계정이 마스터 서버의 msdb 데이터베이스 역할인 TargetServersRole의 멤버여야 합니다.  
  
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
  
#### <a name="to-set-the-service-startup-account-for-sql-server-agent"></a>SQL Server 에이전트에 대한 서비스 시작 계정을 설정하려면  
  
1.  **등록된 서버**에서 더하기 기호를 클릭하여 **데이터베이스 엔진**을 확장합니다.  
  
2.  더하기 기호를 클릭하여 **로컬 서버 그룹** 폴더를 확장합니다.  
  
3.  서비스 시작 계정을 설정하려는 서버 인스턴스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 구성 관리자...** 를 선택합니다.  
  
4.  **사용자 계정 컨트롤** 대화 상자에서 **예**를 클릭합니다.  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구성 관리자의 콘솔 창에서 **SQL Server 서비스**를 선택합니다.  
  
6.  세부 정보 창에서 **SQL Server 에이전트***(server_name)* 를 마우스 오른쪽 단추로 클릭합니다. 여기서 *server_name*은 서비스 시작 계정을 변경하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 인스턴스의 이름입니다. 그런 다음, **속성**을 선택합니다.  
  
7.  **SQL Server 에이전트***(server_name)* **속성** 대화 상자의 **로그온** 탭에 있는 **다음 계정으로 로그온**에서 다음 옵션 중 하나를 선택합니다.  
  
    -   **기본 제공 계정**: 로컬 서버의 리소스만 작업에 필요한 경우 이 옵션을 선택합니다. Windows 기본 제공 계정 유형을 선택하는 방법은 [SQL Server 에이전트 서비스에 대한 계정 선택](http://msdn.microsoft.com/library/ms191543.aspx)을 참조하세요.  
  
        > [!IMPORTANT]  
        > [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스는 **에서** 로컬 서비스 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]계정을 지원하지 않습니다.  
  
    -   **이 계정**: 작업을 수행하는 데 응용 프로그램 리소스를 포함하여 네트워크의 리소스가 필요할 경우나, 다른 Windows 응용 프로그램 로그에 이벤트를 전달하거나, 전자 메일 또는 호출기로 운영자에게 알리려고 할 경우 이 옵션을 선택합니다.  
  
        이 옵션을 선택한 경우:  
  
        1.  **계정 이름** 상자에 SQL Server 에이전트를 실행하기 위해 사용할 계정을 입력합니다. 또는 **찾아보기** 를 클릭하여 **사용자 또는 그룹 선택** 대화 상자를 열고 사용할 계정을 선택합니다.  
  
        2.  **암호** 상자에 계정 암호를 입력합니다. **암호 확인** 상자에 암호를 다시 입력합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구성 관리자에서 **닫기** 단추를 클릭합니다.  
  
