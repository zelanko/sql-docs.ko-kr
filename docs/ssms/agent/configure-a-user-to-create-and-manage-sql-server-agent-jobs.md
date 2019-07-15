---
title: SQL Server 에이전트 작업을 만들고 관리하도록 사용자 구성 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a4f96bac75f76fe6b565dbde2ae4dc0461abd888
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67688706"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configure a User to Create and Manage SQL Server Agent Jobs
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만들거나 실행하도록 사용자를 구성하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  [보안](#Security)  
  
-   **SQL Server 에이전트 작업을 만들고 관리하도록 사용자를 구성하려면 다음을 사용합니다.**  [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Security"></a>보안  
사용자가 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만들거나 실행할 수 있도록 구성하려면 먼저 기존 SQL Server 로그인이나 msdb 역할을 msdb 데이터베이스의 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할 중 하나에 추가해야 합니다. SQLAgentUserRole, SQLAgentReaderRole 또는 SQLAgentOperatorRole.  
  
기본적으로 이러한 데이터베이스 역할의 멤버는 자신의 계정으로 실행되는 고유한 작업 단계를 만들 수 있습니다. 관리 권한이 없는 이러한 사용자가 다른 작업 단계 유형(예: [!INCLUDE[ssIS](../../includes/ssis_md.md)] 패키지)을 실행하는 작업을 실행하려면 프록시 계정에 액세스할 수 있어야 합니다. sysadmin 고정 서버 역할의 모든 멤버에게는 프록시 계정을 만들고 수정하고 삭제할 수 있는 권한이 있습니다. 이러한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할과 관련된 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
#### <a name="Permissions"></a>Permissions  
자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
**SQL Server 에이전트 고정 데이터베이스 역할에 SQL 로그인이나 msdb 역할을 추가하려면**  
  
1.  **개체 탐색기**에서 서버를 확장합니다.  
  
2.  **보안**을 확장한 다음 **로그인**을 확장합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할에 추가하려는 로그인을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
4.  **로그인 속성** 대화 상자의 **사용자 매핑** 에서 **msdb**를 포함하는 행을 선택합니다.  
  
5.  **데이터베이스 역할 멤버 자격: msdb**에서 적합한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할을 선택합니다.  
  
**SQL Server 에이전트 작업 단계를 만들고 관리하는 프록시 계정을 구성하려면**  
  
1.  **개체 탐색기**에서 서버를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장합니다.  
  
3.  **프록시** 를 마우스 오른쪽 단추로 클릭하고 **새 프록시**를 선택합니다.  
  
4.  **새 프록시 계정** 대화 상자의 **일반** 페이지에서 새 프록시의 프록시 이름, 자격 증명 이름 및 설명을 지정합니다. SQL Server 에이전트 프록시를 만들기 전에 자격 증명을 먼저 만들어야 합니다. 자격 증명을 만드는 방법에 대한 자세한 내용은 [방법: 자격 증명 만들기(SQL Server Management Studio)](https://msdn.microsoft.com/c1e77e91-2a69-40d9-b8b3-97cffc710586) 및 [CREATE CREDENTIAL(Transac-SQL)](https://msdn.microsoft.com/d5e9ae69-41d9-4e46-b13d-404b88a32d9d)을 참조하세요.  
  
5.  이 프록시에 대한 적절한 하위 시스템을 선택합니다.  
  
6.  **보안 주체** 페이지에서 프록시 계정에 대한 액세스 권한을 부여 또는 제거할 로그인이나 역할을 추가하거나 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)  
  
