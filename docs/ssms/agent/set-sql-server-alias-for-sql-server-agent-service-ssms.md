---
title: SQL Server 에이전트 서비스에 대한 SQL Server 별칭 설정 | Microsoft 문서
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
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a60a27769f9578c9e10a7f6c2be9dd2b7bff70ae
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 [!INCLUDE[ssDE](../../includes/ssde_md.md)]에 연결하는 데 사용할 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 별칭을 설정하는 방법에 대해 설명합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스는 추가 클라이언트 구성이 필요 없는 동적 서버 이름을 사용하여 명명된 파이프에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 인스턴스에 연결합니다. 기본 네트워크 전송을 사용하지 않는 경우나 다른 명명된 파이프에서 수신하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 인스턴스에 연결 중인 경우에만 서버 연결 별칭을 구성해야 합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   [SQL Server Management Studio를 사용하여 SQL Server 에이전트 서비스에 대한 SQL Server 별칭을 설정하려면](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 로컬 인스턴스를 참조하는 별칭을 선택하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에이전트가 제대로 작동하지 않습니다.  
  
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
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>SQL Server 에이전트 서비스에 대한 SQL Server 별칭을 설정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **SQL Server 에이전트 속성***server_name* 대화 상자의 **페이지 선택**에서 **연결**을 선택합니다.  
  
4.  **로컬 호스트 서버 별칭** 상자에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 연결할 서버의 별칭을 입력합니다.  
  
5.  **확인**을 클릭합니다.  
  
