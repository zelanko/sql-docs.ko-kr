---
description: 커서 함수(Transact-SQL)
title: 커서 함수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cursors
- cursor functions
ms.assetid: 7d9daa10-4c50-4212-9400-42120222b2b8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: feed3d608cf3031d03467b19494dabc7844460fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468089"
---
# <a name="cursor-functions-transact-sql"></a>커서 함수(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

이러한 스칼라 함수는 커서에 대한 정보를 반환합니다.
  
- [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)
- [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)
- [CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)
  
모든 커서 함수는 비결정적입니다. 즉, 이러한 함수가 실행될 때마다 동일한 입력 값 집합을 사용하더라도 항상 동일한 결과가 반환되지는 않습니다. 함수 결정성에 대한 자세한 내용은 [결정적 함수 및 비결정적 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하세요.
  
## <a name="see-also"></a>참고 항목

[기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)
