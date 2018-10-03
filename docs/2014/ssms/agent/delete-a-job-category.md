---
title: 작업 범주 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1e98d9f168e0256b96fefdd1d1c1bf65b5b54155
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078393"
---
# <a name="delete-a-job-category"></a>작업 범주 삭제
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 범주를 삭제하는 방법에 대해 설명합니다.  
  
 작업 범주를 사용하면 작업을 쉽게 필터링하고 그룹화할 수 있게 구성할 수 있습니다. 예를 들어 데이터베이스 유지 관리 범주에 있는 모든 데이터베이스 백업 작업을 구성할 수 있습니다.  
  

  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 사용자가 정의한 작업 범주를 삭제할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 이 작업 범주에 할당된 작업을 다른 작업 범주에 재할당할 것인지 묻습니다. 사용자가 정의한 작업 범주만 삭제할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  

  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-job-category"></a>작업 범주를 삭제하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 작업 범주를 삭제하려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업** 폴더를 마우스 오른쪽 단추로 클릭하고 **작업 범주 관리**를 선택합니다.  
  
4.  **작업 범주 관리***server_name* 대화 상자에서 삭제할 작업 범주를 선택합니다.  
  
5.  **삭제**를 클릭합니다.  
  
6.  **작업 범주** 대화 상자에서 **예**를 클릭합니다.  
  
7.  **작업 범주 관리***server_name* 대화 상자를 닫습니다.  
  

  
##  <a name="TSQL"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-job-category"></a>작업 범주를 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- deletes the job category named AdminJobs.  
    USE msdb ;  
    GO   
    EXEC dbo.sp_delete_category  
        @name = N'AdminJobs',  
        @class = N'JOB' ;  
    GO  
    ```  
  
 자세한 내용은 [sp_delete_category &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-category-transact-sql)합니다.  
  

  
##  <a name="SMO"></a> SQL Server 관리 개체를 사용 하 여  
 **작업 범주를 삭제하려면**  
  
 호출 된 `JobCategory` Visual Basic, Visual C# 또는 PowerShell 등 선택한 프로그래밍 언어를 사용 하 여 클래스입니다.  
  

  
  
