---
title: sp_execute (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_execute
- sp_cursor_execute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute
ms.assetid: 2009acd3-0d92-435a-a8fb-057e50dc7146
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1957103cf2c817f0ef77816446be5fb2d352c9d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124458"
---
# <a name="spexecute-transact-sql"></a>sp_execute(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  준비 된 실행 [!INCLUDE[tsql](../../includes/tsql-md.md)] 지정한 핸들 및 선택적 매개 변수 값을 사용 하 여 문의 합니다. sp_execute가 ID를 지정 하 여 호출 = 12 tabular data TDS (stream) 패킷에서를 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_execute handle OUTPUT  
    [,bound_param  ]  [,...n ]  ]  
```  
  
## <a name="arguments"></a>인수  
 *handle*  
 *처리할* sp_prepare에서 반환 된 값입니다. *처리할* 필요로 하는 필수 매개 변수 **int** 값을 입력 합니다.  
  
 *bound_param*  
 추가 매개 변수의 사용을 나타냅니다. *bound_param* 프로시저에 대 한 추가 매개 변수를 나타내려면 모든 데이터 형식의 입력된 값에 대해 호출 하는 필수 매개 변수입니다.  
  
> [!NOTE]  
>  *bound_param* sp_prepare로 만들어진 선언과 일치 해야 합니다*params* 값 및 형태로 제공 될 수 있습니다  *@name = value* 하거나 *값*합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_prepare &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)  
  
  
