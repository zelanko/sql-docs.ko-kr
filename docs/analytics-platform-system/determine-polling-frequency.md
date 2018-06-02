---
title: 폴링 빈도-분석 플랫폼 시스템 결정 | Microsoft Docs
description: 이 문서에서는 분석 플랫폼 시스템 기기 경고에 대 한 폴링 빈도 결정 하는 방법을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 39597e0e4623a3006709acde7fe54f97545c362f
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707621"
---
# <a name="determine-polling-frequency"></a>폴링 빈도 결정 합니다.
이 문서에서는 분석 플랫폼 시스템 기기 경고에 대 한 폴링 빈도 결정 하는 방법을 설명 합니다.  
  
## <a name="to-determine-the-polling-frequency"></a>폴링 빈도 확인 하려면  
경고가 발생 하면 PDW 사전 알림의 현재 지원 되지 않으므로, 모니터링 솔루션 기기 Dll 폴링을 계속 해야 합니다.  내부적으로 PDW 다른으로 구성 요소를 폴링합니다.  
  
-   클러스터 – 60 초  
  
-   하트 비트-60 초  
  
-   다른 모든 구성 요소-5 분  
  
-   성능 카운터-3 초  
  
도 System Center에서 사용 되는 경고에 대 한 폴링 일반적인 간격은 **15 분 마다**합니다.  물론, 자주 보내거나 가끔 쿼리할 수 있지만 6 시간 마다 미만 폴링 권장 되지 않습니다.  
  
더 자주 폴링은 사용할 수 있지만 너무 자주 폴링 수 복잡해 지는 [sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV 합니다.  너무 자주 폴링 하기가 더 어려운 쿼리 성능을 진단 하는 사용자에 대해 발급 될 때 해당 보기에서 신속 하 게 롤업 합니다.  
  
## <a name="see-also"></a>관련 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](appliance-monitoring.md)  
  
