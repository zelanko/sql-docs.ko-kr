---
title: Transact-SQL 작업 단계 옵션 정의 | Microsoft 문서
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
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: b2a47057-f6fb-432b-a7b6-5d61f33a5d9c
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7296a4a32491dd49af5b4d5ad49ba7ee70655181
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="define-transact-sql-job-step-options"></a>Define Transact-SQL Job Step Options
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서 [!INCLUDE[tsql](../../includes/tsql_md.md)]  [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 에이전트 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 작업 단계에 대한 옵션을 정의하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [보안](#Security)  
  
-   **다음을 사용하여 Transact-SQL 작업 단계 옵션 정의**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Security"></a>보안  
자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-define-transact-sql-job-step-options"></a>Transact-SQL 작업 단계 옵션을 정의하려면  
  
1.  **개체 탐색기**에서 **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 편집할 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
2.  **단계** 페이지를 클릭하고 작업 단계를 클릭한 다음 **편집**을 클릭합니다.  
  
3.  **작업 단계 속성** 대화 상자에서 작업 유형이 **T-SQL(Transact-SQL) 스크립트**임을 확인한 다음 **고급** 페이지를 선택합니다.  
  
4.  **성공한 경우 동작** 목록에서 작업이 성공한 경우에 수행할 동작을 선택합니다.  
  
5.  **다시 시도 횟수** 입력란에 0~9999 사이의 값을 입력하여 다시 시도 횟수를 지정합니다.  
  
6.  **다시 시도 간격(분)** 입력란에 0~9999 사이의 시간(분)을 입력하여 다시 시도 간격을 지정합니다.  
  
7.  **실패한 경우 동작** 목록에서 작업이 실패한 경우에 수행할 동작을 선택합니다.  
  
8.  작업이 [!INCLUDE[tsql](../../includes/tsql_md.md)] 스크립트인 경우 다음 옵션을 선택할 수 있습니다.  
  
    -   **출력 파일**이름을 입력합니다. 기본적으로 작업 단계가 실행될 때마다 파일을 덮어씁니다. 출력 파일을 덮어쓰지 않으려면 **기존 파일에 출력 추가**를 선택합니다. 이 옵션은 **sysadmin** 고정 서버 역할의 멤버만 사용할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 에서는 사용자가 파일 시스템의 임의 파일을 볼 수 없으므로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 를 사용하여 파일 시스템에 기록된 작업 단계 로그를 볼 수 없습니다.  
  
    -   작업 단계를 데이터베이스 테이블에 기록하려면 **테이블에 기록** 을 선택합니다. 기본적으로 작업 단계가 실행될 때마다 테이블 내용을 덮어씁니다. 테이블 내용을 덮어쓰지 않으려면 **테이블의 기존 항목에 출력 추가**를 선택합니다. 작업 단계가 실행된 다음에는 **뷰**를 클릭하여 이 테이블의 내용을 볼 수 있습니다.  
  
    -   출력을 단계 기록에 포함하려면 **기록에 단계 출력 포함** 을 선택합니다. 출력은 오류가 없을 때만 표시됩니다. 또한 출력이 잘릴 수도 있습니다.  
  
9. **sysadmin** 고정 서버 역할의 멤버이면서 이 작업 단계를 다른 SQL 로그인으로 실행하려는 경우 **다음 사용자 이름으로 실행** 목록에서 해당 SQL 로그인을 선택합니다.  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**Transact-SQL 작업 단계 옵션을 정의하려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobStep** 클래스를 사용합니다.  
  
