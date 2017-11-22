---
title: "ROOT 옵션을 사용하여 JSON 출력에 루트 노드 추가(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ROOT (FOR JSON)
ms.assetid: b9afa74a-f59f-483e-a178-42be2e9882c9
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 74af1c3592410fe1ccee740fe07cf21305fe546a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="add-a-root-node-to-json-output-with-the-root-option-sql-server"></a>ROOT 옵션을 사용하여 JSON 출력에 루트 노드 추가(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  단일 최상위 요소를 **FOR JSON** 절의 JSON 출력에 추가하려면 **ROOT** 옵션을 사용합니다.  
  
 **ROOT** 옵션을 지정하지 않은 경우 JSON 출력에는 루트 요소가 포함되지 않습니다.  
  
## <a name="examples"></a>예  
 다음 표에는 **ROOT** 옵션을 사용한 경우와 사용하지 않은 경우 **FOR JSON** 절의 출력이 나와 있습니다.  
  
 다음 표의 예에서는 선택적 *RootName* 인수가 비어 있다고 가정합니다. 루트 요소의 이름을 입력하면 예의 **root** 값이 이 값으로 바뀝니다.  
  
 **ROOT** 옵션을 사용하지 않는 경우  
  
```json  
{  
   <<json properties>>  
}  
```  
  
```json  
[  
   <<json array elements>>  
]  
```  
  
 **ROOT** 옵션을 사용하는 경우  
  
```json  
{   
  "root": {  
   <<json properties>>  
 }  
}  
```  
  
```json  
{   
  "root": [  
   << json array elements >>  
  ]  
}  
```  
  
 아래에는 **ROOT** 옵션을 사용한 **FOR JSON** 절의 다른 예가 나와 있습니다. 이 예에서는 선택적 *RootName* 인수의 값을 지정합니다.  
  
 **Query**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH, ROOT('info')
```  
  
 **결과**  
  
```json  
{
    "info": [{
        "Id": 1,
        "FirstName": "Ken",
        "LastName": "Sánchez",
        "Info": {
            "MiddleName": "J"
        }
    }, {
        "Id": 2,
        "FirstName": "Terri",
        "LastName": "Duffy",
        "Info": {
            "MiddleName": "Lee"
        }
    }, {
        "Id": 3,
        "FirstName": "Roberto",
        "LastName": "Tamburello"
    }, {
        "Id": 4,
        "FirstName": "Rob",
        "LastName": "Walters"
    }, {
        "Id": 5,
        "FirstName": "Gail",
        "LastName": "Erickson",
        "Info": {
            "Title": "Ms.",
            "MiddleName": "A"
        }
    }]
}
```  
  
 **결과(루트 없이)**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.
 
## <a name="see-also"></a>관련 항목:  
 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  
