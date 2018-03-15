---
title: BREAK(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BREAK
- BREAK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- exiting innermost loop [SQL Server]
- END keyword
- ignored statements
- BREAK keyword
ms.assetid: 67c30b8d-3f15-41ad-b9a9-a4ced3b2af9f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9fe4eb7310113a124bee8e1a0f9c4cad3ac45b12
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="break-transact-sql"></a>BREAK(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  WHILE 문의 가장 안쪽의 루프 또는 WHILE 루프 내부의 IF ELSE 문을 종료합니다. 루프의 끝을 표시하는 END 키워드 다음에 표시되는 모든 문은 실행됩니다. BREAK는 IF 테스트에 의해 시작되는 경우가 많습니다.  
  
## <a name="examples"></a>예  
  
```  
-- Uses AdventureWorks  
  
WHILE ((SELECT AVG(ListPrice) FROM dbo.DimProduct) < $300)  
BEGIN  
    UPDATE DimProduct  
        SET ListPrice = ListPrice * 2;  
     IF ((SELECT MAX(ListPrice) FROM dbo.DimProduct) > $500)  
         BREAK;  
END  
```  
  
## <a name="see-also"></a>참고 항목  
 [Control-of-Flow Language&#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [WHILE&#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)   
 [IF...ELSE&#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  


