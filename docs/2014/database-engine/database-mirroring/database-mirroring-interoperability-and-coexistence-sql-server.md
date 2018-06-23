---
title: '데이터베이스 미러링: 상호 운용성 및 공존성 (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2ba2e5af89a4a9eabb420e0d75a8a90b4ef48540
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184325"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>데이터베이스 미러링: 상호 운용성 및 공존성 (SQL Server)
  데이터베이스 미러링은 다음의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]기능 또는 구성 요소와 함께 사용할 수 있습니다.  
  
-   [AlwaysOn 장애 조치 클러스터 인스턴스 (SQL Server 장애 조치 클러스터링)](database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [변경 데이터 캡처 및 변경 내용 추적](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [데이터베이스 스냅숏](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
-   [전체 텍스트 카탈로그](database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [로그 전달](database-mirroring-and-log-shipping-sql-server.md)  
  
-   [복제](database-mirroring-and-replication-sql-server.md)  
  
 데이터베이스 미러링은 다음과 상호 운용되지 않습니다.  
  
-   데이터베이스 간 트랜잭션/분산 트랜잭션  
  
     해당 트랜잭션이 지원되지 않는 이유에 대한 자세한 내용은 [데이터베이스 미러링 또는 AlwaysOn 가용성 그룹에 대해 지원되지 않는 데이터베이스 간 트랜잭션&#40;SQL Server&#41;](../availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)을 참조하세요.  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  