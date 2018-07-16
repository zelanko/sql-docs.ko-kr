---
title: 운영자에게 작업 상태 알리기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26bb76499741ff1448a30ed818bc07e2d96d1928
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181450"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 알림 옵션을 설정하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 작업에 대한 알림을 운영자에게 전송할 수 있도록 하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **운영자에게 작업 상태를 알리려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 관리 개체](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-notify-an-operator-of-job-status"></a>운영자에게 작업 상태를 알리려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 편집할 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **작업 속성** 대화 상자에서 **알림** 페이지를 선택합니다.  
  
4.  전자 메일을 통해 운영자에게 알리려면 **전자 메일**확인란을 선택하고 목록에서 운영자를 선택한 후 다음 중 하나를 선택합니다.  
  
    -   **작업 성공 시** - 작업이 성공적으로 완료되면 운영자에게 알립니다.  
  
    -   **작업 실패 시** - 작업이 성공적으로 완료되지 않았을 때 운영자에게 알립니다.  
  
    -   **작업 완료 시** - 완료 상태에 관계없이 운영자에게 알립니다.  
  
5.  무선 호출기를 통해 운영자에게 알리려면 **호출**확인란을 선택하고 목록에서 운영자를 선택한 후 다음 중 하나를 선택합니다.  
  
    -   **작업 성공 시** - 작업이 성공적으로 완료되면 운영자에게 알립니다.  
  
    -   **작업 실패 시** - 작업이 성공적으로 완료되지 않았을 때 운영자에게 알립니다.  
  
    -   **작업 완료 시** - 완료 상태에 관계없이 운영자에게 알립니다.  
  
6.  Net Send로 운영자에게 알리려면 **Net Send**확인란을 선택하고 목록에서 운영자를 선택한 후 다음 중 하나를 선택합니다.  
  
    -   **작업 성공 시** - 작업이 성공적으로 완료되면 운영자에게 알립니다.  
  
    -   **작업 실패 시** - 작업이 성공적으로 완료되지 않았을 때 운영자에게 알립니다.  
  
    -   **작업 완료 시** - 완료 상태에 관계없이 운영자에게 알립니다.  
  
##  <a name="TSQL"></a> Transact-SQL 사용  
  
#### <a name="to-notify-an-operator-of-job-status"></a>운영자에게 작업 상태를 알리려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'François Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
 자세한 내용은 [sp_add_notification &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)합니다.  
  
##  <a name="SMO"></a> SQL Server 관리 개체를 사용 하 여  
 **운영자에게 작업 상태를 알리려면**  
  
 사용 된 `Job` Visual Basic, Visual C# 또는 PowerShell 등 선택한 프로그래밍 언어를 사용 하 여 클래스입니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](http://msdn.microsoft.com/library/ms162169.aspx)를 참조하세요.  
  
  
