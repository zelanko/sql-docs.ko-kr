---
title: 90 호환성 모드에서 테이블 힌트를 사용할 경우 WITH 키워드를 지정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- table hints [SQL Server]
ms.assetid: 7636cc85-5155-44db-baf6-df807761adb8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff2fee26c6f71cc398f8dbacf91f3ad8dbdb3358
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092154"
---
# <a name="specify-the-with-keyword-when-using-table-hints-in-90-compatibility-mode"></a>호환성 모드 90에서 테이블 힌트를 사용할 경우 WITH 키워드를 지정합니다.
  일부 예외는 있으나 WITH 키워드를 사용하여 테이블 힌트를 지정한 경우에만 쿼리의 FROM 절에서 테이블 힌트가 지원됩니다. 자세한 내용은[!INCLUDE[tsql](../../includes/tsql-md.md)]온라인 설명서에서 "FROM([!INCLUDE[tsql](../../includes/tsql-md.md)])" 및 "테이블 힌트( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )"를 참조하십시오.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 테이블 힌트 앞에 WITH 키워드를 포함하여 FROM 절에서 테이블 힌트가 들어 있는 쿼리를 수정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
