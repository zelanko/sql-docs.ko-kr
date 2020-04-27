---
title: Sysperfinfo에서 bigint 값을 필요로 하도록 응용 프로그램을 수정 합니다. cntr_value | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sysperfinfo
- bigint values [SQL Server]
ms.assetid: b0345303-6e9a-4078-8148-6e1bce207b8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ced1e07b5423dcdc7c13d24e8528a2b6ac240aaa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093957"
---
# <a name="modify-applications-to-expect-bigint-values-from-sysperfinfocntr_value"></a>sysperfinfo.cntr_value에서 bigint 값을 예상할 수 있도록 애플리케이션을 수정합니다.
  sysperfinfo cntr_value 열 `bigint` 에 대 한 값을 반환 합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 cntr_value 열의 `bigint` 값을 처리할 수 있도록 sysperfinfo를 사용하는 애플리케이션을 수정합니다.  
  
> [!NOTE]  
>  sysperfinfo는 호환성 뷰입니다. sys.dm_os_performance_counter 동적 관리 뷰를 대신 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
