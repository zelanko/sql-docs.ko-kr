---
title: 폴링 빈도-Analytics Platform System 결정 | Microsoft Docs
description: 이 문서에는 분석 플랫폼 시스템 어플라이언스 경고에 대 한 폴링 빈도 결정 하는 방법을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: eec9e3e211c68b7f56fe6829a70064317b96e646
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52519571"
---
# <a name="determine-polling-frequency"></a>폴링 빈도 결정 합니다.
이 문서에는 분석 플랫폼 시스템 어플라이언스 경고에 대 한 폴링 빈도 결정 하는 방법을 설명 합니다.  
  
## <a name="to-determine-the-polling-frequency"></a>폴링 빈도 확인 하려면  
경고가 발생할 경우 PDW 사전 알림의 현재 지원 되지 않으므로, 모니터링 솔루션에 Dll 어플라이언스 폴링을 계속 해야 합니다.  내부적으로 PDW 다른 간격으로 구성 요소를 폴링합니다.  
  
-   클러스터-60 초  
  
-   하트 비트-60 초  
  
-   다른 모든 구성 요소-5 분  
  
-   성능 카운터-3 초  
  
또한 System Center에서 사용 되는 경고에 대 한 폴링 하려면 일반적인 간격이 **15 분 마다**합니다.  물론 자주 보내거나 가끔 쿼리할 수 있지만 6 시간 미만 마다 폴링 권장 되지 않습니다.  
  
더 자주 폴링은 사용할 수 있지만 너무 자주 폴링 복잡 하 게 합니다 [sys.dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV 합니다.  너무 자주 폴링을 수행 하기가 더 어려운 쿼리 성능을 진단 하는 작업을 할 때 문제가 해당 보기에서 신속 하 게 롤업.  
  
## <a name="see-also"></a>관련 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[어플라이언스 모니터링 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
