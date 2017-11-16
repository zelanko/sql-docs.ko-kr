---
title: "JSON에 Null 값 포함 - INCLUDE_NULL_VALUES 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- INCLUDE_NULL_VALUES (FOR JSON)
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 732fd945099a13d1e6f319db3e0f5ac48e370346
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="include-null-values-in-json---includenullvalues-option"></a>JSON에 Null 값 포함 - INCLUDE_NULL_VALUES 옵션
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 절의 JSON 출력에 null 값을 포함하려면 **INCLUDE_NULL_VALUES** 옵션을 지정합니다.  
  
 **INCLUDE_NULL_VALUES** 옵션을 지정하지 않은 경우 JSON 출력은 쿼리 결과에서 null인 값에 대한 속성을 포함하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에는 **INCLUDE_NULL_VALUES** 옵션을 사용한 경우와 사용하지 않은 경우 **FOR JSON** 절의 출력이 나와 있습니다.  
  
|**INCLUDE_NULL_VALUES** 옵션을 사용하지 않는 경우|**INCLUDE_NULL_VALUES** 옵션을 사용하는 경우|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 아래에는 **INCLUDE_NULL_VALUES** 옵션을 사용한 **FOR JSON** 절의 다른 예제가 나와 있습니다.  
  
 **Query**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES    
```  
  
 **결과**  
  
```json  
[{
    "name": "John",
    "surname": null
}, {
    "name": "Jane",
    "surname": "Doe"
}] 
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.  

## <a name="see-also"></a>관련 항목:  
 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

