---
title: "커서 함수 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cursors
- cursor functions
ms.assetid: 7d9daa10-4c50-4212-9400-42120222b2b8
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7cbeb217f4803da10e52e62074dbd42821b1e21
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="cursor-functions-transact-sql"></a>커서 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

다음 스칼라 함수는 커서에 대한 정보를 반환합니다.
  
|||  
|-|-|  
|[@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)|[CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)|  
|[@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)||  
  
모든 커서 함수는 비결정적입니다. 이는 이러한 함수를 호출할 때마다 동일한 입력 값 집합을 사용하더라도 항상 동일한 결과가 반환되지는 않는다는 것을 의미합니다. 함수 결정성에 대 한 자세한 내용은 참조 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)합니다.
  
## <a name="see-also"></a>참고 항목
[기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)
  
  

