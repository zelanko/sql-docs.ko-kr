---
title: sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4aa1fd4418e4758ca41cce9d3aeba70838a0dce0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260409"
---
# <a name="run-transact-sql-script-files-using-sqlcmd"></a>sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행
  `sqlcmd`를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일을 실행할 수 있습니다. A [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일이 조합을 포함할 수 있는 텍스트 파일로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 `sqlcmd` 명령 및 스크립팅 변수입니다.  
  
 메모장을 사용하여 간단한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일을 만들려면 다음 단계를 따르십시오.  
  
1.  **시작**을 클릭하고 **모든 프로그램**, **보조프로그램**을 차례로 가리킨 다음 **메모장**을 클릭합니다.  
  
2.  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 복사하여 메모장에 붙여 넣습니다.  
  
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
  
### <a name="to-run-the-script-file"></a>스크립트 파일을 실행하려면  
  
1.  명령 프롬프트 창을 엽니다.  
  
2.  명령 프롬프트 창에서 다음을 입력 합니다. `sqlcmd -S myServer\instanceName -i C:\myScript.sql`  
  
3.  Enter 키를 누릅니다.  
  
 명령 프롬프트 창에 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 직원의 이름 및 주소 목록이 출력됩니다.  
  
### <a name="to-save-this-output-to-a-text-file"></a>텍스트 파일에 이 출력을 저장하려면  
  
1.  명령 프롬프트 창을 엽니다.  
  
2.  명령 프롬프트 창에서 다음을 입력 합니다. `sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt`  
  
3.  Enter 키를 누릅니다.  
  
 출력이 명령 프롬프트 창에 반환되는 대신 EmpAdds.txt 파일에 보내집니다. EmpAdds.txt 파일을 열어서 이 출력을 확인할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sqlcmd 유틸리티 시작](sqlcmd-start-the-utility.md)   
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)  
  
  
