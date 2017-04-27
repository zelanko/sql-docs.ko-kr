---
title: "운영자 편집 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, operators
- modifying operators
- jobs [SQL Server Agent], operators
- operators (users) [Database Engine], modifying with Management Studio
ms.assetid: b2ba2168-ca0b-4b59-9007-4e1e4c30679e
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b8628cf736650c53493501777f79f970ff864209
ms.lasthandoff: 04/11/2017

---
# <a name="edit-an-operator"></a>운영자 편집
이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql_md.md)]에서 알림 메시지 수신을 위한 운영자의 응답 가능 여부와 전자 메일, 호출기 및 Net Send 주소를 편집하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전에:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **다음을 사용하여 운영자를 편집합니다.**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
  
-   **이후 버전에서는** 에이전트에서 호출기 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] net send [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]옵션이 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
-   SQL Server 에이전트는 데이터베이스 메일을 사용하여 운영자에게 전자 메일 및 호출기 알림을 보내도록 구성해야 합니다. 자세한 내용은 [경고를 운영자에게 할당](http://msdn.microsoft.com/library/ms190038.aspx)을 참조하세요.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 는 작업 구조를 만들고 관리할 수 있는 바람직한 방법을 제공하는데 이는 그래픽을 사용하여 쉽게 작업을 관리할 수 있는 방법입니다.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
**sysadmin** 고정 서버 역할의 멤버만이 운영자를 편집할 수 있습니다.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-edit-an-operator"></a>운영자를 편집하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 편집하려는 운영자가 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **운영자** 폴더를 확장합니다.  
  
4.  편집하려는 운영자를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
    *operator_name***속성** 대화 상자에 포함된 사용 가능한 옵션에 대한 자세한 내용은 다음을 참조하십시오.  
  
    -   [운영자 속성 - 새 운영자&amp;#40;일반 페이지&amp;#41;](../../ssms/agent/operator-properties-new-operator-general-page.md)  
  
    -   [운영자 속성 - 새 운영자&amp;#40;알림 페이지&amp;#41;](../../ssms/agent/operator-properties-new-operator-notifications-page.md)  
  
    -   [운영자 속성&amp;#40;기록 페이지&amp;#41;](../../ssms/agent/operator-properties-history-page.md)  
  
5.  완료되었으면 **확인**을 클릭합니다.  
  
## <a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-edit-an-operator"></a>운영자를 편집하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- updates the operator status to enabled, and sets the days   
    -- (from Monday through Friday, from 8 A.M. through 5 P.M.)
    --  when the operator can be paged.   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_operator   
        @name = N'François Ajenstat',  
        @enabled = 1,  
        @email_address = N'françoisa',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 64 ;  
    GO  
    ```  
  
자세한 내용은 [sp_update_operator(Transact-SQL)](http://msdn.microsoft.com/en-us/231750a6-4828-4d03-afe6-b91d38c42ed3)를 참조하세요.  
  

