---
title: 90 이상 호환성 모드에서는 외부 조인 연산자 *= 및 =* 가 지원 되지 않습니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: 62a6f9e016abf24f28660b04e7a6242fdd6606ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093692"
---
# <a name="outer-join-operators--and--are-not-supported-in-90-or-later-compatibility-modes"></a>호환성 모드 90 이상에서는 외부 조인 연산자 \*= 및 =\*가 지원되지 않습니다.
  업그레이드 관리자가 외부 조인 연산자 \*= 및 =\*를 사용 하는 것을 감지 했습니다. 호환성 모드가 90 이상일 때는 이러한 연산자가 지원되지 않습니다. 업그레이드할 때 사용자 데이터베이스는 호환성 모드를 유지합니다. 이러한 연산자를 사용하는 문은 실패합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 데이터베이스 호환성 모드를 90 이상으로 변경 하기 전에 외부 조인 연산자 \*= 및 =\* 를 사용 하는 문을 수정 하 여 해당 하는 outer join 키워드를 사용 합니다. 다음 예에서는 `\*=` 연산자를 사용하는 쿼리와 `LEFT OUTER JOIN` 키워드를 사용하는 동일한 쿼리를 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
