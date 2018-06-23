---
title: Sysperfinfo.cntr_value에서 bigint 값을 기대 하는 응용 프로그램은 수정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sysperfinfo
- bigint values [SQL Server]
ms.assetid: b0345303-6e9a-4078-8148-6e1bce207b8c
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 436e4d7dc8f1e4a98cfab2b0f2ce2c77576950f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089226"
---
# <a name="modify-applications-to-expect-bigint-values-from-sysperfinfocntrvalue"></a>sysperfinfo.cntr_value에서 bigint 값을 예상할 수 있도록 응용 프로그램을 수정합니다.
  sysperfinfo 반환는 `bigint` cntr_value 열에 대 한 값입니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 cntr_value 열의 `bigint` 값을 처리할 수 있도록 sysperfinfo를 사용하는 응용 프로그램을 수정합니다.  
  
> [!NOTE]  
>  sysperfinfo가 호환성 뷰이므로 합니다. sys.dm_os_performance_counter 동적 관리 뷰를 대신 사용해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
