---
title: "명시적 스키마와 함께 OPENJSON 사용(SQL Server) | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OPENJSON, with explicit schema
ms.assetid: 9c1c3bfb-e1ad-4659-b94f-722b0848d5a2
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9909c0d9d42e40e09517d60bb23906a49c8e9161
ms.lasthandoff: 04/11/2017

---
# <a name="use-openjson-with-an-explicit-schema-sql-server"></a>명시적 스키마와 함께 JSON 사용(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **OPENJSON** 을 명시적 스키마와 함께 사용하면 WITH 절에서 지정하는 대로 서식이 지정된 테이블이 반환됩니다.  
  
 아래에는 명시적 스키마와 함께 **OPENJSON** 을 사용하는 몇 가지 예가 나와 있습니다. 자세한 내용 및 더 많은 예제를 보려면 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.  
  
## <a name="example---use-the-with-clause-to-format-the-output"></a>예 - WITH 절을 사용하여 출력의 서식 지정  
 다음 쿼리는 아래 표에 나와 있는 결과를 반환합니다. AS JSON 절을 사용하는 경우 col5 및 array_element에서 스칼라 값이 아닌 JSON 개체로 값이 반환됩니다.  
  
```tsql  
DECLARE @json NVARCHAR(MAX) =
N'{"someObject":   
    {"someArray":  
      [  
          {"k1": 11, "k2": null, "k3": "text"},  
          {"k1": 21, "k2": "text2", "k4": { "data": "text4" }},  
          {"k1": 31, "k2": 32},  
          {"k1": 41, "k2": null, "k4": { "data": false }}     
       ]  
    }  
 }'  
   
SELECT * FROM  
 OPENJSON(@json, N'lax $.someObject.someArray')  
WITH ( k1 int,   
        k2 varchar(100),  
        col3 varchar(6) N'$.k3',  
        col4 varchar(10) N'lax $.k4.data',  
        col5 nvarchar(MAX) N'lax $.k4' AS JSON, 
        array_element nvarchar(MAX) N'$' AS JSON  
 )  
```  
  
 **결과**  
  
|k1|k2|col3|col4|col5|array_element|  
|--------|--------|----------|----------|----------|--------------------|  
|11|*NULL*|"text"|*NULL*|*NULL*|{"k1": 11, "k2": null, "k3": "text"}|  
|21|"text2"|*NULL*|"text4"|{ "data": "text4" }|{"k1": true, "k2": "text2", "k4": { "data": "text4" } }|  
|31|"32"|*NULL*|*NULL*|*NULL*|{"k1": 31, "k2": 32 }|  
|41|*NULL*|*NULL*|false|{ "data": false }|{"k1": 41, "k2": null,       "k4": { "data": false }    }|  
  
## <a name="example---load-json-into-a-includessnoversionincludesssnoversion-mdmd-table"></a>예 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 JSON 로드  
 다음 예에는 전체 JSON 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 로드합니다.  
  
```tsql  
DECLARE @json NVARCHAR(MAX) = '{  
  "id" : 2,  
  "firstName": "John",  
  "lastName": "Smith",  
  "isAlive": true,  
  "age": 25,  
  "dateOfBirth": "2015-03-25T12:00:00",  
  "spouse": null  
  }';  
   
  INSERT INTO Person  
  SELECT *   
  FROM OPENJSON(@json)  
  WITH (id int,  
        firstName nvarchar(50), lastName nvarchar(50),   
        isAlive bit, age int,  
        dateOfBirth datetime2, spouse nvarchar(50))  
```  
  
## <a name="see-also"></a>참고 항목  
 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  

