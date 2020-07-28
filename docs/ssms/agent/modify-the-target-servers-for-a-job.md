---
title: Modify the Target Servers for a Job
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- modifying target servers
- SQL Server Agent jobs, target servers
- target servers [SQL Server], modifying
ms.assetid: 9dbe24f2-acec-4aa2-920c-e8e96efa18e4
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5cb213fa8d51950d33565c0e4e0339d32d18339b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715757"
---
# <a name="modify-the-target-servers-for-a-job"></a>Modify the Target Servers for a Job

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 에이전트 작업의 대상 서버를 변경하는 방법에 대해 설명합니다.

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
sysadmin 고정 서버 역할의 멤버는 기본적으로 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 msdb 데이터베이스의 다음 SQL Server 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
1.  **SQLAgentUserRole**  
  
2.  **SQLAgentReaderRole**  
  
3.  SQLAgentOperatorRole  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>작업의 대상 서버를 변경하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **작업 속성** 대화 상자에서 **대상**페이지를 선택하고 **대상 로컬 서버**또는 **대상 다중 서버**를 클릭합니다.  
  
    **대상 다중 서버**를 선택한 경우 서버 이름 왼쪽에 있는 확인란을 선택하여 작업 대상으로 사용할 서버를 지정합니다. 작업 대상으로 지정하지 않을 서버의 확인란 선택이 취소되어 있는지 확인합니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>작업의 대상 서버를 변경하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde_md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 다중 서버 작업 Weekly Sales Backups를 SEATTLE2 서버에 할당합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',   
    @server_name = N'SEATTLE2' ;   
GO  
```  
  
자세한 내용은 [sp_add_jobserver(Transact-SQL)](https://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[기업 내 관리 자동화](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
