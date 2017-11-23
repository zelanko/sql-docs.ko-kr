---
title: sp_execute (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_execute
- sp_cursor_execute_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_execute
ms.assetid: 2009acd3-0d92-435a-a8fb-057e50dc7146
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2b40bd51a730cf902068aa0ba8bc40411f002f3b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spexecute-transact-sql"></a>sp_execute(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  준비 된 실행 [!INCLUDE[tsql](../../includes/tsql-md.md)] 지정한 핸들 및 선택적 매개 변수 값을 사용 하 여 문을 합니다. sp_execute가 ID를 지정 하 여 호출 = 표 형식 데이터 TDS (stream) 패킷의 12입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_execute handle OUTPUT  
    [,bound_param  ]  [,...n ]  ]  
```  
  
## <a name="arguments"></a>인수  
 *핸들*  
 이 *처리* sp_prepare에서 반환 된 값입니다. *처리* 필요로 하는 필수 매개 변수 **int** 값을 입력 합니다.  
  
 *bound_param*  
 추가 매개 변수의 사용을 나타냅니다. *bound_param* 필수 매개 변수는 프로시저에 대 한 추가 매개 변수를 나타내려면 모든 데이터 형식의 입력된 값에 대 한 호출입니다.  
  
> [!NOTE]  
>  *bound_param* 은 sp_prepare로 만들어진 선언과 일치 해야*params* 값 형태로 수 있으며  *@name = value* 또는 *값*합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_prepare &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)  
  
  
