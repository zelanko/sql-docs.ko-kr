---
title: AlwaysOn 가용성 그룹 (SQL Server)에 대 한 TRANSACT-SQL 문 개요 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: 184d0a81-2259-4db9-9d0d-01aac0b502c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b0c766ed98bf5833790d2c0c1a35bfbff3c91e3c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208863"
---
# <a name="overview-of-transact-sql-statements-for-alwayson-availability-groups-sql-server"></a>AlwaysOn 가용성 그룹에 대한 Transact-SQL 문 개요(SQL Server)
  이 항목에서는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 배포와 지정된 가용성 그룹, 가용성 복제본 및 가용성 데이터베이스의 생성 및 관리를 지원하는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 문을 소개합니다.  
  
  
##  <a name="CreateEndpoint"></a> CREATE ENDPOINT  
 [CREATE ENDPOINT … FOR DATABASE_MIRRORING](/sql/t-sql/statements/create-endpoint-transact-sql) 은 데이터베이스 미러링 엔드포인트(서버 인스턴스에 없는 경우)를 만듭니다. ph x="1" /&gt; 또는 데이터베이스 미러링을 배포할 각 서버 인스턴스에는 데이터베이스 미러링 엔드포인트가 필요합니다.  
  
 엔드포인트를 만들 서버 인스턴스에서 이 문을 실행합니다. 지정된 서버 인스턴스에 데이터베이스 미러링 엔드포인트를 하나만 만들 수 있습니다. 자세한 내용은 [데이터베이스 미러링 엔드포인트&amp;#40;SQL Server&amp;#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)을 참조하세요.  
  
##  <a name="CreateAG"></a> CREATE AVAILABILITY GROUP  
 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql) 은 새 가용성 그룹을 만들고 선택적으로 가용성 그룹 수신기를 만듭니다. 최소한 초기 주 복제본이 될 로컬 서버 인스턴스는 지정해야 합니다. 선택적으로 최대 네 개의 보조 복제본을 지정할 수도 있습니다.  
  
 새 가용성 그룹의 초기 주 복제본을 호스팅할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 CREATE AVAILABILITY GROUP을 실행합니다. 이 서버 인스턴스는 Windows Server 장애 조치 클러스터 (WSFC)의 노드에 있어야 합니다 (자세한 내용은 [필수 조건, 제한 사항 및 AlwaysOn 가용성 그룹에 대 한 권장 사항 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)합니다.  
  
##  <a name="AlterAG"></a> ALTER AVAILABILITY GROUP  
 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 은 기존 가용성 그룹 또는 가용성 그룹 수신기를 변경하고 가용성 그룹의 장애 조치(Failover)를 수행할 수 있도록 지원합니다.  
  
 현재 주 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 ALTER AVAILABILITY GROUP을 실행합니다.  
  
##  <a name="AlterDb"></a> ALTER DATABASE … SET HADR …  
 ALTER DATABASE 문의 [SET HADR](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) 절의 옵션을 통해 보조 데이터베이스를 해당 주 데이터베이스의 가용성 그룹에 조인하고, 조인된 데이터베이스를 제거하고, 조인된 데이터베이스에서 데이터 동기화를 일시 중지하고, 데이터 동기화를 다시 시작할 수 있습니다.  
  
##  <a name="DropAG"></a> DROP AVAILABILITY GROUP  
 [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) 은 지정된 가용성 그룹과 모든 복제본을 제거합니다. DROP AVAILABILITY GROUP은 WSFC 장애 조치(failover) 클러스터의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 노드에서 실행될 수 있습니다.  
  
##  <a name="Restrictions"></a> Restrictions on the AVAILABILITY GROUP Transact-SQL Statements  
 CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP 및 DROP AVAILABILITY GROUP [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문은 다음과 같은 제한 사항이 있습니다.  
  
-   DROP AVAILABILITY GROUP을 제외하고 이러한 문을 실행하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 HADR 서비스를 사용하도록 설정해야 합니다. 자세한 내용은 [AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
-   이러한 문은 트랜잭션 또는 일괄 처리 내에서 실행할 수 없습니다.  
  
-   이러한 문은 장애가 발생한 후 해결을 위해 최선을 다하지만 모든 변경 사항에 대한 롤백을 보장하지는 않습니다. 그러나, 시스템에서 부분 장애를 깨끗하게 처리한 다음 무시할 수 있어야 합니다.  
  
-   이러한 문은 식 또는 변수를 지원하지 않습니다.  
  
-   다른 가용성 그룹 동작 또는 복구가 진행 중인 동안 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행하면 오류가 반환됩니다. 이 경우 동작 또는 복구가 완료될 때까지 기다렸다가 필요한 경우 문을 다시 시도하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
