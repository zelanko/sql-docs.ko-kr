---
title: "운영자에게 경고 할당 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, operators
- assigning alerts to operator
- SQL Server Agent, alerts
- alerts [SQL Server], assigning to operator
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: aa818155-6fa2-4565-a09f-5c7e31c89754
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1f12a64b87badd99d7cf38dd248326c005ed6d2f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="assign-alerts-to-an-operator"></a>운영자에게 경고 할당
이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql_md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 운영자들이 작업에 대한 알림을 받을 수 있도록 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 경고를 운영자에게 할당하는 방법을 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전에:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **다음을 사용하여 운영자에게 경고를 할당합니다.**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 는 그래픽 방식으로 전체 경고 시스템을 간편하게 관리할 수 있도록 해 줍니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 를 사용하면 경고 인프라를 쉽게 구성할 수 있습니다.  
  
-   경고에 대한 응답으로 알림을 보내려면 먼저 메일을 보낼 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트를 구성해야 합니다. 자세한 내용은 [Configure SQL Server Agent Mail to Use Database Mail](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)을 참조하세요.  
  
-   전자 메일 메시지 또는 호출기 알림을 전송하는 동안 오류가 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 오류 로그에 오류가 보고됩니다.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
**sysadmin** 고정 서버 역할의 멤버만 운영자에 경고를 할당할 수 있습니다.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-assign-alerts-to-an-operator"></a>운영자에게 경고를 할당하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 경고를 할당하려는 운영자가 포함된 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **운영자** 폴더를 확장합니다.  
  
4.  경고를 할당하려는 운영자를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 후 **알림** 페이지를 선택합니다.  
  
5.  *operator_name***속성** 대화 상자의 **페이지 선택**에서 **알림**을 선택합니다.  
  
6.  **사용자에게 알림을 보내는 방법**아래에서 **경고** 를 선택하여 이 운영자에게 보내진 경고 목록을 보거나 **작업** 을 선택하여 이 운영자에게 알림을 보내는 작업 목록을 봅니다. **전자 메일**, **호출기**또는 **Net send**중 하나 이상의 확인란을 선택하여 필요에 따라 각 알림에 대한 알림 방법을 정의합니다.  
  
7.  완료되었으면 **확인**을 클릭합니다.  
  
## <a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-assign-alerts-to-an-operator"></a>운영자에게 경고를 할당하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert)  
    -- This example assumes that Test Alert already exists
    -- and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
자세한 내용은 [sp_add_notification(Transact-SQL)](http://msdn.microsoft.com/en-us/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)을 참조하세요.  
  
