---
title: 외부 조인 연산자 *= 및 =* 호환성 모드 90 이상에서 지원 되지 않는 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- =* join
- '*= join'
- joins [SQL Server]
ms.assetid: ca4aa11f-1048-411f-9c6c-3d0a8e319f2f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01584c368f9af43a8e63ec04d3eaf4f9228d9c96
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582199"
---
# <a name="outer-join-operators--and--are-not-supported-in-90-or-later-compatibility-modes"></a>호환성 모드 90 이상에서는 외부 조인 연산자 \*= 및 =\*가 지원되지 않습니다.
  업그레이드 관리자 외부 조인 연산자의 사용을 발견 했습니다. \*= 및 =\*합니다. 호환성 모드가 90 이상일 때는 이러한 연산자가 지원되지 않습니다. 업그레이드할 때 사용자 데이터베이스는 호환성 모드를 유지합니다. 이러한 연산자를 사용하는 문은 실패합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 데이터베이스 호환성 모드가 90 이상으로 변경 하기 전에 외부 조인 연산자를 사용 하는 문을 수정 \*= 및 =\* 동일한 OUTER JOIN 키워드를 사용 하도록 합니다. 다음 예에서는 `\*=` 연산자를 사용하는 쿼리와 `LEFT OUTER JOIN` 키워드를 사용하는 동일한 쿼리를 보여 줍니다.  
  
```  
-- This query uses an old-style outer join operator.  
USE pubs  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee, jobs   
WHERE employee.job_id *= jobs.job_id  
ORDER BY employee.job_id  
  
-- This query uses the ANSI standard keywords LEFT OUTER JOIN.  
USE pubs;  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
ORDER BY employee.job_id  
```  
  
 외부 조인에 대한 자세한 내용은 SQL Server 온라인 설명서에서 "외부 조인 사용"을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
