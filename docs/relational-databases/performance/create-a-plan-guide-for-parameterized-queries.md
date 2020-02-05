---
title: 매개 변수가 있는 쿼리를 위한 계획 지침 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- parameterized queries, plan guides for
- plan guides [SQL Server], parameterized queries
ms.assetid: b532ae16-66e7-4641-9bc8-b0d805853477
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 45a57f45eae2a54d73e08064b9a02446871f8400
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67946952"
---
# <a name="create-a-plan-guide-for-parameterized-queries"></a>매개 변수가 있는 쿼리를 위한 계획 지침 만들기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  TEMPLATE 계획 지침은 지정된 형식으로 매개 변수화되는 독립 실행형 쿼리와 일치합니다.  
  
 다음 예에서는 지정된 형식으로 매개 변수화되는 쿼리와 일치하는 계획 지침을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 쿼리를 매개 변수화하도록 지정합니다. 다음 두 개의 쿼리는 구문이 같고 상수 리터럴 값만 다릅니다.  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 매개 변수가 있는 쿼리 형식에 대한 계획 지침은 다음과 같습니다.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 앞의 예에서 `@stmt` 매개 변수의 값은 매개 변수가 있는 쿼리 형식입니다. sp_create_plan_guide에서 사용하기 위해 이 값을 얻는 안정적인 한 가지 방법은 [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) 시스템 저장 프로시저를 사용하는 것입니다. 다음 스크립트는 매개 변수가 있는 쿼리를 얻고 이에 대한 계획 지침을 만들기 위해 사용할 수 있습니다.  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  `@stmt` 에 전달된 `sp_get_query_template` 매개 변수에 있는 상수 리터럴 값은 리터럴을 대체하는 매개 변수에 대해 선택한 데이터 형식에 영향을 미칠 수 있습니다. 이는 계획 지침 일치에도 영향을 미칩니다. 둘 이상의 계획 지침을 만들어 서로 다른 매개 변수 값 범위를 처리해야 할 수도 있습니다.  
  
 또한 TEMPLATE 계획 지침은 SQL 계획 지침과도 함께 사용할 수 있습니다. 예를 들어 쿼리 클래스가 매개 변수화되도록 TEMPLATE 계획 지침을 만들 수 있습니다. 그런 다음 매개 변수가 있는 해당 쿼리 형식에 대한 SQL 계획 지침을 만들 수 있습니다.  
  
  
