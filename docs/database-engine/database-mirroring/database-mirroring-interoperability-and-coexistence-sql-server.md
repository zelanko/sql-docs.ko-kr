---
title: '데이터베이스 미러링: 상호 운용성 및 공존성 (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 60b393377747df8da93690d5820c2e46d4a7132c
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35311812"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>데이터베이스 미러링: 상호 운용성 및 공존성 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  데이터베이스 미러링은 다음의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]기능 또는 구성 요소와 함께 사용할 수 있습니다.  
  
-   [Always On 장애 조치(failover) 클러스터 인스턴스(SQL Server 장애 조치(failover) 클러스터링)](../../database-engine/database-mirroring/database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [변경 데이터 캡처 및 변경 내용 추적](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [데이터베이스 스냅숏](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
-   [전체 텍스트 카탈로그](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [로그 전달](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)  
  
-   [복제](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
 데이터베이스 미러링은 다음과 상호 운용되지 않습니다.  
  
-   데이터베이스 간 트랜잭션/분산 트랜잭션  
  
     해당 트랜잭션이 지원되지 않는 이유에 대한 자세한 내용은 [Always On 가용성 그룹 및 데이터베이스 미러링에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)을 참조하세요.  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
