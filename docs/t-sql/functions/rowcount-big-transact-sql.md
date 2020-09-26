---
description: ROWCOUNT_BIG(Transact-SQL)
title: ROWCOUNT_BIG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ROWCOUNT_BIG
- ROWCOUNT_BIG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ROWCOUNT_BIG function
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 6e18a0eb-bb36-4348-90d9-8b1ecf095064
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 124ba59b2942fcfa7c4ac26be7b24df35c75806a
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379979"
---
# <a name="rowcount_big-transact-sql"></a>ROWCOUNT_BIG(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  최근 실행한 문의 영향을 받은 행 수를 반환합니다. 이 함수는 ROWCOUNT_BIG의 반환 유형이 **bigint**라는 점만 제외하고 [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md)처럼 작동합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ROWCOUNT_BIG ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 **bigint**  
  
## <a name="remarks"></a>설명  
 SELECT 문을 실행한 후 이 함수를 실행하면 SELECT 문에서 반환한 행 수를 반환합니다.  
  
 INSERT, UPDATE 또는 DELETE 문을 실행한 후 이 함수를 실행하면 데이터 수정 문의 영향을 받은 행 수를 반환합니다.  
  
 행을 반환하지 않는 문(예를 들어 IF 문)을 실행한 후 이 함수를 실행하면 0을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [COUNT_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/count-big-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
