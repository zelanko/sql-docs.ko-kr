---
title: "구성 함수 (Transact SQL) | Microsoft Docs"
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
- functions [SQL Server], configuration
- configuration options [SQL Server], functions
- current configuration information
- configuration functions [SQL Server]
ms.assetid: 066f15e7-3406-437e-93c4-3f247c529169
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1e1187ab7240e32ab6fb571deaa620532fbf9c1f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="configuration-functions-transact-sql"></a>구성 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

다음 스칼라 함수는 현재의 구성 옵션 설정에 대한 정보를 반환합니다.
  
|||  
|-|-|  
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|[@@OPTIONS](../../t-sql/functions/options-transact-sql.md)|  
|[@@DBTS](../../t-sql/functions/dbts-transact-sql.md)|[@@REMSERVER](../../t-sql/functions/remserver-transact-sql.md)|  
|[@@LANGID](../../t-sql/functions/langid-transact-sql.md)|[@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|[@@SERVICENAME](../../t-sql/functions/servicename-transact-sql.md)|  
|[@@LOCK_TIMEOUT](../../t-sql/functions/lock-timeout-transact-sql.md)|[@@SPID](../../t-sql/functions/spid-transact-sql.md)|  
|[@@MAX_CONNECTIONS](../../t-sql/functions/max-connections-transact-sql.md)|[@@TEXTSIZE](../../t-sql/functions/textsize-transact-sql.md)|  
|[@@MAX_PRECISION](../../t-sql/functions/max-precision-transact-sql.md)|[@@VERSION](../../t-sql/functions/version-transact-sql-configuration-functions.md)|  
|[@@NESTLEVEL](../../t-sql/functions/nestlevel-transact-sql.md)||  
  
모든 구성 함수가 결정적이지는 않습니다. 이는 이러한 함수를 호출할 때마다 동일한 입력 값 집합을 사용하더라도 항상 동일한 결과가 반환되지는 않는다는 것을 의미합니다. 함수 결정성에 대 한 자세한 내용은 참조 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)합니다.
  
## <a name="see-also"></a>참고 항목
[함수 &#40; Transact SQL &#41;](../../t-sql/functions/functions.md)
  
  

