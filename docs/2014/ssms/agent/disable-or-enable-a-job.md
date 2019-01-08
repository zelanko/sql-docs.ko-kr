---
title: 작업을 사용하지 않거나 사용하도록 설정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- stopping jobs
- disabling jobs
- SQL Server Agent jobs, disabling
- jobs [SQL Server Agent], disabling
ms.assetid: 5041261f-0c32-4d4a-8bee-59a6c16200dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1fa9a2700bd2f6a9ce2b074b1633182fc30c9aa7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816915"
---
# <a name="disable-or-enable-a-job"></a>작업을 사용하지 않거나 사용하도록 설정
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]에이전트 작업을 비활성화하는 방법에 대해 설명합니다. 작업을 사용하지 않도록 설정하더라도 해당 작업은 삭제되지 않으며 필요할 때 사용하도록 설정할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **작업을 사용하지 않거나 사용하도록 설정하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-disable-or-enable-a-job"></a>작업을 사용하지 않거나 사용하도록 설정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업**을 확장한 다음 사용하지 않거나 사용하도록 설정할 작업을 마우스 오른쪽 단추로 클릭합니다.  
  
4.  작업을 사용하지 않도록 설정하려면 **사용 안 함**을 클릭합니다. 작업을 사용하도록 설정하려면 **사용**을 클릭합니다.  
  
##  <a name="TSQL"></a> Transact-SQL 사용  
  
#### <a name="to-disable-or-enable-a-job"></a>작업을 사용하지 않거나 사용하도록 설정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- changes the name, description, and enables status of the job NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @new_name = N'NightlyBackups -- Disabled',  
        @description = N'Nightly backups disabled during server migration.',  
        @enabled = 1 ;  
    GO  
    ```  
  
 자세한 내용은 [sp_update_job &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)합니다.  
  
  
