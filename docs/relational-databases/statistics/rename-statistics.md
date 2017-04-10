---
title: "통계 이름 바꾸기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-statistics"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "통계 이름 바꾸기"
  - "통계 [SQL Server], 이름 바꾸기"
ms.assetid: a3bed7b7-3dc5-4b33-b1c6-67c27f573764
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# 통계 이름 바꾸기
  다음을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 통계 개체의 이름을 바꾸려면 사용합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 통계 개체의 이름을 바꾸려면**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
 기본적으로 인덱스를 만들면 해당 인덱스의 키 열에 통계가 만들어집니다. 따라서 색인의 이름을 바꿀 경우 통계 개체의 이름이 자동으로 바뀌고 그 반대의 경우에도 마찬가지입니다.  
  
 개체 이름의 일부를 변경하면 스크립트나 저장 프로시저가 작동되지 않을 수 있습니다. 이름을 바꾸는 것보다 통계 개체를 삭제하고 새로운 이름으로 다시 만드는 것이 좋습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### 통계 개체의 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_rename N'AK_Employee_LoginID', N'AK_Emp_Login', N'STATISTICS';   
    GO  
    ```  
  
 자세한 내용은 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)을 참조하세요.  
  
  