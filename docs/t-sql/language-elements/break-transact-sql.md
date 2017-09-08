---
title: "나누기 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ac7f12956aa0f8e2919aa33cf3d3cd8df140b96
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="break-transact-sql"></a>BREAK(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
  
## <a name="see-also"></a>관련 항목:  
 [흐름 제어 언어 &#40; Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [반면 &#40; Transact SQL &#41;](../../t-sql/language-elements/while-transact-sql.md)   
 [IF...ELSE&#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  



