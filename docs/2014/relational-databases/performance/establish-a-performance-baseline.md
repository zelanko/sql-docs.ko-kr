---
title: 성능 기준선 설정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], baselines
- monitoring performance [SQL Server], baselines
- tuning databases [SQL Server], baselines
- server performance [SQL Server], baselines
- performance [SQL Server], baselines
- baseline performance [SQL Server]
- measurements for baseline statistics [SQL Server]
- monitoring server performance [SQL Server], establishing baseline
- database monitoring [SQL Server], baselines
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4b382545e9f7e5af1607d67539f2ae9f29cfdce3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774555"
---
# <a name="establish-a-performance-baseline"></a>성능 기준선 설정
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템이 최적으로 실행되고 있는지 판단하려면 먼저 시간을 두고 정기적으로 서버의 성능을 측정하여 서버 성능 기준선을 설정해야 합니다. 그런 다음 이전에 측정한 값과 각 새 집합을 비교합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]성능에 영향을 미치는 요소는 다음과 같습니다.  
  
-   시스템 리소스(하드웨어)  
  
-   네트워크 아키텍처  
  
-   운영 체제  
  
-   데이터베이스 애플리케이션  
  
-   클라이언트 애플리케이션  
  
 다음은 기준선 측정을 사용해 확인할 수 있는 기본 사항입니다.  
  
-   작업량이 많을 때와 많지 않을 때  
  
-   프로덕션 쿼리 또는 일괄 처리 명령 응답 시간  
  
-   데이터베이스 백업 및 복구 완료 시간  
  
 서버 성능 기준선을 설정한 후 현재 서버의 성능을 기준선 통계와 비교하십시오. 기준선과 지나치게 많은 차이가 나면 더 자세하게 조사해야 합니다. 이것은 해당 영역에 대한 튜닝 또는 재구성이 필요함을 의미할 수 있습니다. 예를 들어 쿼리 집합을 실행하는 시간이 늘어나면 쿼리를 검사하여 다시 작성할 수 있는지 확인하거나 열 통계 또는 새 인덱스를 추가해야 하는지 확인할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
