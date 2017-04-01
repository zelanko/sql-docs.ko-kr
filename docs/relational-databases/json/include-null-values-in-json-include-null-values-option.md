---
title: "INCLUDE_NULL_VALUES 옵션을 사용하여 JSON 출력으로 Null 값 포함(SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "INCLUDE_NULL_VALUES(FOR JSON)"
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 13
---
# INCLUDE_NULL_VALUES 옵션을 사용하여 JSON 출력으로 Null 값 포함(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 절의 JSON 출력에 null 값을 포함하려면 **INCLUDE_NULL_VALUES** 옵션을 지정합니다.  
  
 **INCLUDE_NULL_VALUES** 옵션을 지정하지 않은 경우 JSON 출력은 쿼리 결과에서 null인 값에 대한 속성을 포함하지 않습니다.  
  
## 예  
 다음 예제에는 **INCLUDE_NULL_VALUES** 옵션을 사용한 경우와 사용하지 않은 경우 **FOR JSON** 절의 출력이 나와 있습니다.  
  
|**INCLUDE_NULL_VALUES** 옵션을 사용하지 않는 경우|**INCLUDE_NULL_VALUES** 옵션을 사용하는 경우|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 아래에는 **INCLUDE_NULL_VALUES** 옵션을 사용한 **FOR JSON** 절의 다른 예제가 나와 있습니다.  
  
 **Query**  
  
```tsql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES  
```  
  
 **결과**  
  
```json  
[   
   {"name": "John",  "surname": null },  
   {"name": "Jane",  "surname": "Doe"}  
]  
```  
  
## 참고 항목  
 [FOR 절&#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  