---
title: 데이터베이스 간 트랜잭션이 지원 되지 데이터베이스 미러링 또는 AlwaysOn 가용성 그룹 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c3616e40ff54c67d27902ddf9454084fb62e282
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813658"
---
# <a name="cross-database-transactions-not-supported-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>데이터베이스 미러링 또는 AlwaysOn 가용성 그룹에 대해 지원되지 않는 데이터베이스 간 트랜잭션(SQL Server)
  데이터베이스 간 트랜잭션 또는 분산 트랜잭션은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 또는 데이터베이스 미러링에서 지원되지 않습니다. 이는 다음과 같은 이유로 인해 트랜잭션 원자성/무결성을 보장할 수 없기 때문입니다.  
  
-   데이터베이스 간 트랜잭션의 경우: 각 데이터베이스는 독립적으로 커밋합니다. 따라서 단일 가용성 그룹에 있는 데이터베이스의 경우에도 한 데이터베이스에서 트랜잭션을 커밋한 후 다른 데이터베이스가 커밋하기 전에 장애 조치(failover)가 발생할 수 있습니다. 데이터베이스 미러링의 경우 장애 조치(failover) 후 미러된 데이터베이스가 일반적으로 다른 데이터베이스와 다른 서버 인스턴스에 있으며, 두 데이터베이스가 동일한 두 파트너 사이에서 미러된 경우에도 두 데이터베이스가 동시에 장애 조치를 실행한다고 보장할 수 없으므로 이 문제가 더 복잡해집니다.  
  
-   분산 트랜잭션의 경우: 장애 조치 후 새 주 서버/주 복제본을 이전 주 서버/주 복제본에서 distributed transaction coordinator에 연결할 아닙니다. 따라서 새 주 서버/주 복제본은 해당 트랜잭션 상태를 가져올 수 없습니다.  
  
 다음 데이터베이스 미러링 예에서는 논리적 불일치가 발생하는 방식을 보여 줍니다. 이 예에서 애플리케이션은 데이터베이스 간 트랜잭션을 사용하여 두 행의 데이터를 삽입합니다. 한 행은 미러된 데이터베이스 A의 테이블에 삽입되고 다른 행은 데이터베이스 B의 테이블에 삽입됩니다. 데이터베이스 A는 자동 장애 조치(failover) 있는 보호 우선 모드로 미러됩니다. 트랜잭션이 커밋되는 동안 데이터베이스 A를 사용할 수 없게 되고 미러링 세션이 자동으로 데이터베이스 A의 미러로 장애 조치됩니다.  
  
 장애 조치 후에 데이터베이스 B에서는 데이터베이스 간 트랜잭션이 성공적으로 커밋될 수 있지만 장애 조치된 데이터베이스에서는 커밋되지 않습니다. 데이터베이스 A의 원래 주 서버가 실패하기 전에 데이터베이스 간 트랜잭션 로그를 미러 서버로 보내지 않은 경우 이런 문제가 발생합니다. 장애 조치 후에 새로운 주 서버에는 해당 트랜잭션이 없습니다. 데이터베이스 B에 삽입한 데이터는 그대로 유지되고 데이터베이스 A에 삽입한 데이터는 손실되었으므로 데이터베이스 A와 B가 일치하지 않습니다.  
  
 MS DTC 트랜잭션을 사용하는 동안 이와 유사한 시나리오가 발생할 수 있습니다. 예를 들어 장애 조치 후에 새로운 주 서버가 MS DTC에 연결합니다. 그러나 MS DTC는 새로운 주 서버를 알지 못하며 다른 데이터베이스에서 커밋된 것으로 간주되는 "커밋 준비 중"인 모든 트랜잭션을 종료합니다.  
  
> [!IMPORTANT]  
>  데이터베이스 미러링 또는 가용성 그룹을 DTC와 함께 사용하는 경우 SQL Server 설치가 지원되지 않는 문제가 발생하지 않습니다. 그러나 데이터베이스가 데이터베이스 미러링 세션 또는 가용성 그룹의 일부이고 DTC도 데이터베이스에서 사용되는 경우에는 데이터베이스 미러링 또는 가용성 그룹과 DTC를 함께 사용하는 것과 무관할 때만 Microsoft에서 지원 문제를 조사합니다.  
  
  
