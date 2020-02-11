---
title: 폴링 주기 확인
description: 이 문서에서는 분석 플랫폼 시스템 어플라이언스 경고에 대 한 폴링 빈도를 결정 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 005fe3d14a7314f7339157064b248a81044a1dfb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401211"
---
# <a name="determine-polling-frequency"></a>폴링 빈도 결정
이 문서에서는 분석 플랫폼 시스템 어플라이언스 경고에 대 한 폴링 빈도를 결정 하는 방법을 설명 합니다.  
  
## <a name="to-determine-the-polling-frequency"></a>폴링 빈도를 확인 하려면  
PDW는 경고 발생 시 현재 사전 알림을 지원 하지 않으므로 모니터링 솔루션은 어플라이언스 Dll을 지속적으로 폴링합니다.  내부적으로 PDW는 서로 다른 간격으로 구성 요소를 폴링합니다.  
  
-   클러스터-60 초  
  
-   하트 비트-60 초  
  
-   기타 모든 구성 요소-5 분  
  
-   성능 카운터-3 초  
  
시스템 센터 에서도 사용 되는 경고를 폴링하는 일반적인 간격은 **15 분**입니다.  분명히 또는 덜 자주 쿼리를 할 수 있지만, 6 시간 이내에 폴링 하지 않는 것이 좋습니다.  
  
더 자주 폴링하는 것이 가능 하지만, 너무 자주 폴링은 [dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV를 복잡 하 게 만들 수 있습니다.  너무 자주 폴링하는 경우 사용자가 신속 하 게 뷰를 사용할 수 없을 때 쿼리 성능 문제를 진단 하기 어려울 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](appliance-monitoring.md)  
  
