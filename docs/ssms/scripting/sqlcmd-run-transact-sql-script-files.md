---
title: sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행
ms.custom: seo-lt-2019
ms.date: 07/15/2016
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ed85470d8e054ba60ae0b2525f773f83d70d0da3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75253207"
---
# <a name="sqlcmd---run-transact-sql-script-files"></a>sqlcmd - Transact-SQL 스크립트 파일 실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 **sqlcmd** 를 사용하여 Transact-SQL 스크립트 파일을 실행합니다. Transact-SQL 스크립트 파일은 Transact-SQL 문, **sqlcmd** 명령 및 스크립팅 변수의 조합을 포함할 수 있는 텍스트 파일입니다.  

## <a name="create-a-script-file"></a>스크립트 파일 만들기  
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
  
## <a name="run-the-script-file"></a>스크립트 파일 실행  
  
1.  명령 프롬프트 창을 엽니다.  
  
2.  명령 프롬프트 창에 **sqlcmd -S myServer\instanceName -i C:\myScript.sql**을 입력합니다.  
  
3.  Enter 키를 누릅니다.  
  
 명령 프롬프트 창에 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 직원의 이름 및 주소 목록이 출력됩니다.  

## <a name="save-the-output-to-a-text-file"></a>텍스트 파일로 출력을 저장합니다.
  
1.  명령 프롬프트 창을 엽니다.  
  
2.  명령 프롬프트 창에 **sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt**를 입력합니다.  
  
3.  Enter 키를 누릅니다.  
  
 출력이 명령 프롬프트 창에 반환되는 대신 EmpAdds.txt 파일에 보내집니다. EmpAdds.txt 파일을 열어서 이 출력을 확인할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [sqlcmd 유틸리티 시작](../../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)  
  
  
