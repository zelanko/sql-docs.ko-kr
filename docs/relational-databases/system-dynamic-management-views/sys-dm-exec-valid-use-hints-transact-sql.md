---
title: sys.dm_exec_valid_use_hints (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: d1fb0ffed04c77e280d02378429cf769107bdfbc
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34463599"
---
# <a name="sysdmexecvalidusehints-transact-sql"></a>sys.dm_exec_valid_use_hints (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

반환 [USE 힌트](../../t-sql/queries/hints-transact-sql-query.md) 힌트 이름을 지원 합니다. 행당 하나의 힌트 이름을 나열합니다.  
  
이 DMV를 사용 하 여 사용 하 여 힌트 표기법에서 모든 지원 되는 힌트의 목록을 볼 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|힌트의 이름입니다.|

참조 [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md) 각 힌트에 대 한 설명입니다.

에 도입 된 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] s p 1입니다.
  
## <a name="see-also"></a>관련 항목:  
    
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

