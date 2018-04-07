---
title: 폴링 빈도 (분석 플랫폼 시스템)를 결정 합니다.
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 062c0e3d-f7d0-44f1-aeab-a9bd17dc6fdd
caps.latest.revision: 7
ms.openlocfilehash: e67ab38c12000f3d78a9179a177ce5f673b8eaa2
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="determine-polling-frequency"></a>폴링 빈도 결정 합니다.
이 항목에서는 SQL Server PDW 어플라이언스에 경고에 대 한 폴링 빈도 결정 하는 방법에 설명 합니다.  
  
## <a name="to-determine-the-polling-frequency"></a>폴링 빈도 확인 하려면  
경고가 발생 하면 PDW 사전 알림의 현재 지원 되지 않으므로, 모니터링 솔루션 기기 Dll 폴링을 계속 해야 합니다.  내부적으로 PDW 다른으로 구성 요소를 폴링합니다.  
  
-   클러스터 – 60 초  
  
-   하트 비트-60 초  
  
-   다른 모든 구성 요소-5 분  
  
-   성능 카운터-3 초  
  
도 System Center에서 사용 되는 경고에 대 한 폴링 일반적인 간격은 **15 분 마다**합니다.  물론, 자주 보내거나 가끔 쿼리할 수 있지만 6 시간 마다 미만 폴링 권장 되지 않습니다.  
  
더 자주 폴링은 사용할 수 있지만 너무 자주 폴링 수 복잡해 지는 [sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV 합니다.  이 어려울 수 있습니다 쿼리 성능 문제를 진단 하는 경우 사용자가 있는 빠르게 쿼리 보기 롤업 합니다.  
  
## <a name="see-also"></a>관련 항목:  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](appliance-monitoring.md)  
  
