---
title: 하나 이상의 작업 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, deleting
- dropping jobs
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 67dcdad0-57b2-431c-b77f-4ffc926af93d
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 98721e58322867b942703fc245115b497ad79c34
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172312"
---
# <a name="delete-one-or-more-jobs"></a>하나 이상의 작업 삭제
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 삭제하는 방법에 대해 설명합니다.  
  
 
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 **sysadmin** 고정 서버 역할의 멤버가 아닌 경우 자신이 소유한 작업만 삭제할 수 있습니다.  
  
 
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-job"></a>작업을 삭제하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 삭제할 작업을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
3.  **개체 삭제** 대화 상자에서 삭제할 작업이 선택되었는지 확인합니다.  
  
4.  **확인**을 클릭합니다.  
  
#### <a name="to-delete-multiple-jobs"></a>여러 작업을 삭제하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업 활동 모니터**를 마우스 오른쪽 단추로 클릭한 다음 **작업 활동 보기**를 클릭합니다.  
  
4.  작업 활동 모니터에서 삭제할 작업을 선택하고 마우스 오른쪽 단추로 클릭한 다음 **작업 삭제**를 선택합니다.  
  

  
##  <a name="TSQL"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-job"></a>작업을 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_job  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 자세한 내용은 참조 [sp_delete_job &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql)합니다.  
  

  
##  <a name="SMO"></a> SQL Server Management Objects를 사용 하 여  
 **여러 작업을 삭제하려면**  
  
 사용 하 여 `JobCollection` Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용 하 여 클래스입니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](http://msdn.microsoft.com/library/ms162169.aspx)를 참조하세요.  
  

  
  
