---
title: 병목 상태 식별 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource bottlenecks [SQL Server]
- database monitoring [SQL Server], bottlenecks
- performance [SQL Server], bottlenecks
- tuning databases [SQL Server], bottlenecks
- monitoring server performance [SQL Server], bottlenecks
- monitoring performance [SQL Server], bottlenecks
- database performance [SQL Server], bottlenecks
- server performance [SQL Server], bottlenecks
- bottlenecks [SQL Server]
- identifying bottlenecks [SQL Server]
ms.assetid: db079e65-ee80-4105-aec9-f8230d0d6635
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 213df75d1883de730a0231c009f1d178814ed463
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370645"
---
# <a name="identify-bottlenecks"></a>병목 상태 식별
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  공유 리소스를 동시에 액세스하는 경우 병목 상태가 발생합니다. 일반적으로 병목 상태는 모든 소프트웨어 시스템에서 필연적으로 나타나지만 공유 리소스에 대한 과도한 요구는 응답 시간을 현저히 늦추는 원인이므로 반드시 확인하고 적절하게 튜닝해야 합니다.  
  
 병목 상태의 원인은 다음과 같습니다.  
  
-   리소스가 부족하여 구성 요소 추가나 업그레이드가 필요한 경우  
  
-   같은 유형의 리소스에 작업이 골고루 분산되지 않은 경우 (예를 들어 하나의 디스크가 독점된 경우)  
  
-   리소스가 잘못 동작하는 경우  
  
-   리소스가 잘못 구성된 경우  
  
## <a name="analyzing-bottlenecks"></a>병목 상태 분석  
 다양한 이벤트에서 과도하게 시간이 소요되면 튜닝할 수 있는 병목 상태가 있음을 의미합니다.  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
-   다른 구성 요소로 인해 이 구성 요소에 로드가 도달하지 못해 로드를 완료하기까지의 시간이 길어지는 경우  
  
-   네트워크 정체로 인해 클라이언트 요청에 소요되는 시간이 길어지는 경우  
  
 다음은 서버 성능을 추적하고 병목 상태를 확인할 때 모니터링하는 5개의 중요 영역입니다.  
  
|병목 상태가 발생할 수 있는 영역|서버에 미치는 영향|  
|------------------------------|---------------------------|  
|메모리 사용|Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 할당된 메모리나 사용할 수 있는 메모리가 부족하면 성능이 저하됩니다. 이 경우 데이터를 데이터 캐시에서 직접 읽지 못하고 디스크에서 읽어야 합니다. 또한 Microsoft Windows 운영 체제에서 페이지가 필요할 때마다 디스크와 데이터를 스왑하면서 페이징을 과도하게 수행할 수 있습니다.|  
|CPU 사용량|CPU 사용량이 장기간 높은 상태로 유지되면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 튜닝이나 CPU 업그레이드가 필요할 수 있습니다.|  
|디스크 I/O(입/출력)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 인덱스를 사용하는 등의 방법으로 쿼리를 튜닝하여 불필요한 I/O를 줄일 수 있습니다.|  
|사용자 연결|너무 많은 사용자가 동시에 서버에 액세스하는 경우 성능이 저하될 수 있습니다.|  
|차단 잠금|잘못 설계된 애플리케이션은 잠금을 일으키고 동시성을 제한하여 결과적으로 응답 시간을 길어지고 트랜잭션 처리율이 낮아질 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [CPU 사용량 모니터링](../../relational-databases/performance-monitor/monitor-cpu-usage.md)   
 [디스크 사용량 모니터링](../../relational-databases/performance-monitor/monitor-disk-usage.md)   
 [메모리 사용량 모니터링](../../relational-databases/performance-monitor/monitor-memory-usage.md)   
 [SQL Server, General Statistics 개체](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)   
 [SQL Server, Locks 개체](../../relational-databases/performance-monitor/sql-server-locks-object.md)  
  
  
