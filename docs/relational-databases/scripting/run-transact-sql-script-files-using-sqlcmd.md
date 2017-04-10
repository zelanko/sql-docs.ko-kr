---
title: "sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행 | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "transact sql 스크립트"
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
caps.latest.revision: 42
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행
 **sqlcmd**를 사용하여 Transact-SQL 스크립트 파일을 실행합니다. Transact-SQL 스크립트 파일은 Transact-SQL 문, **sqlcmd** 명령 및 스크립팅 변수의 조합을 포함할 수 있는 텍스트 파일입니다.  

## 스크립트 파일 만들기  
 메모장을 사용하여 간단한 Transact-SQL 스크립트 파일을 만들려면 다음 단계를 따르세요.  
  
1.  **시작**을 클릭하고 **모든 프로그램**, **보조프로그램**을 차례로 가리킨 다음 **메모장**을 클릭합니다.  
  
2.  다음 Transact-SQL 코드를 복사하여 메모장에 붙여넣습니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT p.FirstName + ' ' + p.LastName AS 'Employee Name',  
    a.AddressLine1, a.AddressLine2 , a.City, a.PostalCode   
    FROM Person.Person AS p   
       INNER JOIN HumanResources.Employee AS e   
            ON p.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.BusinessEntityAddress bea   
            ON bea.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.Address AS a   
            ON a.AddressID = bea.AddressID;  
    GO  
    ```  
  
3.  C 드라이브에 **myScript.sql** 이라는 이름으로 파일을 저장합니다.  
  
## 스크립트 파일 실행  
  
1.  명령 프롬프트 창을 엽니다.  
  
2.  명령 프롬프트 창에 **sqlcmd -S myServer\instanceName -i C:\myScript.sql**을 입력합니다.  
  
3.  Enter 키를 누릅니다.  
  
 명령 프롬프트 창에 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 직원의 이름 및 주소 목록이 출력됩니다.  

## 텍스트 파일로 출력을 저장합니다.
  
1.  명령 프롬프트 창을 엽니다.  
  
2.  명령 프롬프트 창에 **sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt**를 입력합니다.  
  
3.  Enter 키를 누릅니다.  
  
 출력이 명령 프롬프트 창에 반환되는 대신 EmpAdds.txt 파일에 보내집니다. EmpAdds.txt 파일을 열어서 이 출력을 확인할 수 있습니다.  
  
## 참고 항목  
 [sqlcmd 유틸리티 시작](../../relational-databases/scripting/start-the-sqlcmd-utility.md)   
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)  
  
  