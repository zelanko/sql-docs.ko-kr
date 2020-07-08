---
title: sys. dm_exec_valid_use_hints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_valid_use_hints
- sys.dm_exec_valid_use_hints_TSQL
- dm_exec_valid_use_hints
- dm_exec_valid_use_hints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_valid_use_hints management view
ms.assetid: 65d50589-39c2-4046-92b6-0c4587d8c593
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5bcc9db1f2ff0b4395a68025e54b719dc25c31cd
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053466"
---
# <a name="sysdm_exec_valid_use_hints-transact-sql"></a>sys. dm_exec_valid_use_hints (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

Use [hint](../../t-sql/queries/hints-transact-sql-query.md#use_hint) 지원 힌트 이름을 반환 합니다. 행 마다 하나의 힌트 이름을 나열 합니다.  
  
이 DMV를 사용 하 여 USE 힌트 표기법에서 지원 되는 모든 힌트의 목록을 볼 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|힌트의 이름입니다.|

각 힌트에 대 한 설명은 [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint) 를 참조 하세요.

S p 1에서 도입 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 되었습니다.
  
## <a name="see-also"></a>참고 항목  
    
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

