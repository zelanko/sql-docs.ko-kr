---
title: 외래 키 관계 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- foreign keys [SQL Server], deleting
- removing foreign keys
- deleting foreign keys
ms.assetid: 9c9e9ae4-9e03-4137-acb6-b18928a0c4ca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 919a0c9eb96021ccd7495579cda9756bcdde3194
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761442"
---
# <a name="delete-foreign-key-relationships"></a>외래 키 관계 삭제
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 외래 키 제약 조건을 삭제할 수 있습니다. 외래 키 제약 조건을 삭제하면 참조 무결성을 적용할 필요가 없어집니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **외래 키 제약 조건을 삭제하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-foreign-key-constraint"></a>FOREIGN KEY 제약 조건을 삭제하려면  
  
1.  **개체 탐색기**에서 제약 조건을 포함하는 테이블을 확장하고 **키**를 확장합니다.  
  
2.  제약 조건을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
3.  **개체 삭제** 대화 상자에서 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-foreign-key-constraint"></a>FOREIGN KEY 제약 조건을 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE dbo.DocExe   
    DROP CONSTRAINT FK_Column_B;   
    GO  
    ```  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)을 참조하세요.  
  
  
