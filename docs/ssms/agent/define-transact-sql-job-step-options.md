---
title: Define Transact-SQL Job Step Options
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: b2a47057-f6fb-432b-a7b6-5d61f33a5d9c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8dffd043dcd03d73dda9964ee050fcb262dc2b07
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242515"
---
# <a name="define-transact-sql-job-step-options"></a>Define Transact-SQL Job Step Options
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에이전트 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 작업 단계에 대한 옵션을 정의하는 방법에 대해 설명합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-define-transact-sql-job-step-options"></a>Transact-SQL 작업 단계 옵션을 정의하려면  
  
1.  **개체 탐색기**에서 **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 편집할 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
2.  **단계** 페이지를 클릭하고 작업 단계를 클릭한 다음 **편집**을 클릭합니다.  
  
3.  **작업 단계 속성** 대화 상자에서 작업 유형이 **T-SQL(Transact-SQL) 스크립트**임을 확인한 다음 **고급** 페이지를 선택합니다.  
  
4.  **성공한 경우 동작** 목록에서 작업이 성공한 경우에 수행할 동작을 선택합니다.  
  
5.  **다시 시도 횟수** 입력란에 0~9999 사이의 값을 입력하여 다시 시도 횟수를 지정합니다.  
  
6.  **다시 시도 간격(분)** 입력란에 0~9999 사이의 시간(분)을 입력하여 다시 시도 간격을 지정합니다.  
  
7.  **실패한 경우 동작** 목록에서 작업이 실패한 경우에 수행할 동작을 선택합니다.  
  
8.  작업이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트인 경우 다음 옵션을 선택할 수 있습니다.  
  
    -   **출력 파일**이름을 입력합니다. 기본적으로 작업 단계가 실행될 때마다 파일을 덮어씁니다. 출력 파일을 덮어쓰지 않으려면 **기존 파일에 출력 추가**를 선택합니다. 이 옵션은 **sysadmin** 고정 서버 역할의 멤버만 사용할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 사용자가 파일 시스템의 임의 파일을 볼 수 없으므로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 파일 시스템에 기록된 작업 단계 로그를 볼 수 없습니다.  
  
    -   작업 단계를 데이터베이스 테이블에 기록하려면 **테이블에 기록** 을 선택합니다. 기본적으로 작업 단계가 실행될 때마다 테이블 내용을 덮어씁니다. 테이블 내용을 덮어쓰지 않으려면 **테이블의 기존 항목에 출력 추가**를 선택합니다. 작업 단계가 실행된 다음에는 **뷰**를 클릭하여 이 테이블의 내용을 볼 수 있습니다.  
  
    -   출력을 단계 기록에 포함하려면 **기록에 단계 출력 포함** 을 선택합니다. 출력은 오류가 없을 때만 표시됩니다. 또한 출력이 잘릴 수도 있습니다.  
  
9. **sysadmin** 고정 서버 역할의 멤버이면서 이 작업 단계를 다른 SQL 로그인으로 실행하려는 경우 **다음 사용자 이름으로 실행** 목록에서 해당 SQL 로그인을 선택합니다.  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>SQL Server 관리 개체 사용  
**Transact-SQL 작업 단계 옵션을 정의하려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobStep** 클래스를 사용합니다.  
  
