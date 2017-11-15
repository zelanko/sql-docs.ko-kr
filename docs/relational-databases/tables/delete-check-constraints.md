---
title: "CHECK 제약 조건 삭제 | Microsoft 문서"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing constraints
- CHECK constraints, deleting
- constraints [SQL Server], deleting
- constraints [SQL Server], check
- deleting constraints
ms.assetid: 5f86c1a6-f5fa-4e77-a892-f6ae96fc0ab3
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 93863660e64e67571a0412ffe0494c8c64670924
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="delete-check-constraints"></a>CHECK 제약 조건 삭제
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 CHECK 제약 조건을 삭제할 수 있습니다. CHECK 제약 조건을 삭제하면 제약 조건 식에 포함된 하나 이상의 열에 입력할 수 있는 데이터 값에 대한 제한 사항이 제거됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **CHECK 제약 조건을 삭제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-check-constraint"></a>CHECK 제약 조건을 삭제하려면  
  
1.  **개체 탐색기**에서 CHECK 제약 조건이 있는 테이블을 확장합니다.  
  
2.  **제약 조건**을 확장합니다.  
  
3.  제약 조건을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
4.  **개체 삭제** 대화 상자에서 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-check-constraint"></a>CHECK 제약 조건을 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    ALTER TABLE dbo.DocExc   
    DROP CONSTRAINT CHK_ColumnD_DocExc;  
    GO  
    ```  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
  
