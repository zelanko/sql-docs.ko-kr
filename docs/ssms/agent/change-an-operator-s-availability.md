---
title: 운영자의 응답 가능 여부 변경 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- canceling operators
- reactivating operators
- removing operators
- deleting operators
- available operators [SQL Server]
- dropping operators
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
- disabling operators
- operators (users) [Database Engine], changing availability with Management Studio
ms.assetid: 10d58b92-b67b-47e2-af9c-9f9fd6968bba
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8f1ef4382c49ed30e8792c504e3cd554bf1535cf
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51701801"
---
# <a name="change-an-operator39s-availability"></a>운영자의 응답 가능 여부 변경
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 운영자의 경고 알림 수신 일정을 변경하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [보안](#Security)  
  
-   **운영자의 응답 가능 여부를 변경하려면:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
**sysadmin** 고정 서버 역할의 멤버만이 운영자를 편집할 수 있습니다.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-change-an-operators-availability"></a>운영자의 응답 가능 여부를 변경하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 사용하거나 사용하지 않도록 설정할 운영자가 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **운영자** 폴더를 확장합니다.  
  
4.  사용하거나 사용하지 않도록 설정할 운영자를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음 **일반** 탭을 클릭합니다.  
  
5.  _operator\_name_**속성** 대화 상자에서 **사용** 확인란을 선택하거나 선택을 취소합니다.  
  
6.  **확인**을 클릭합니다.  
  
## <a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-change-an-operators-availability"></a>운영자의 응답 가능 여부를 변경하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- disables the 'François Ajenstat' operator  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_operator   
        @name = N'François Ajenstat',  
        @enabled = 0;  
    GO  
    ```  
  
자세한 내용은 [sp_update_operator(Transact-SQL)](https://msdn.microsoft.com/231750a6-4828-4d03-afe6-b91d38c42ed3)를 참조하세요.  
  
