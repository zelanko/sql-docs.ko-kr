---
title: 작업 범주 정보 나열 | Microsoft 문서
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 231143d7b7fb90f8da6a614d047b98f9da22dbb0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078756"
---
# <a name="list-job-category-information"></a>작업 범주 정보 나열
  작업 범주 정보를 나열 하는 방법을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 SQL Server 관리 개체.  

  
##  <a name="Security"></a> 보안  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  

  
##  <a name="TSQL"></a> Transact-SQL 사용  
  
#### <a name="to-list-job-category-information"></a>작업 범주 정보를 나열하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 자세한 내용은 참조 [sp_help_category &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql)합니다.  
  
  
##  <a name="SMO"></a> SQL Server Management Objects를 사용 하 여  
 **작업 범주 정보를 나열하려면**  
  
 사용 하 여 `JobCategory` Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용 하 여 클래스... 자세한 내용은 참조 [SQL Server Management Objects &#40;SMO&#41; 프로그래밍 가이드](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)합니다.  
  
  
  
