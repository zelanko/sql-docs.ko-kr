---
title: SQL Server 모니터 개요 | Microsoft Docs
description: SQL Server 모니터에 대해 알아봅니다. SQL Server 복제 모니터 및 데이터베이스 미러링 모니터 모듈을 사용하는 방법을 알아봅니다. 사용에 필요한 권한을 살펴봅니다.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlservermonitor.main.f1
helpviewer_keywords:
- SQL Server Monitor [SQL Server]
ms.assetid: 048ae16d-31c3-489a-9f1e-1400a3bacd39
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1bb99ef49e22c578ec1ebd8cc715a6e70e5bb6df
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771797"
---
# <a name="sql-server-monitor-overview"></a>SQL Server 모니터 개요
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  SQL Server 모니터는 모니터링 기능을 수행하지 않지만 이 기능을 수행하는 모듈을 호스팅합니다. SQL Server 모니터 모듈에는 복제 모니터와 데이터베이스 미러링 모니터가 있습니다.  
  
 이러한 모듈 중 하나를 사용하려면 **이동** 메뉴에서 해당 모듈을 선택합니다. 현재 선택한 모듈에서 탐색 창과 세부 정보 창의 내용, 세부 정보 창의 사용자 상호 작용, 내용과 상태에 대한 쿼리 등을 소유합니다.  
  
> [!NOTE]  
>  이러한 모니터에 대한 자세한 내용은 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication.md) 및 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
  
-   복제 모니터  
  
     복제를 모니터링하려면 배포자에서 **sysadmin** 고정 서버 역할의 멤버이거나 배포 데이터베이스에서 **replmonitor** 고정 데이터베이스 역할의 멤버여야 합니다. 시스템 관리자는 사용자를 **replmonitor** 역할에 추가할 수 있으며 이렇게 하면 해당 사용자가 복제 모니터에서 복제 작업을 볼 수 있습니다. 이때 사용자가 복제를 관리할 수는 없습니다.  
  
-   데이터베이스 미러링 모니터  
  
     데이터베이스 미러링을 모니터링하려면 서버 인스턴스에서 **sysadmin** 고정 서버 역할 또는 **dbm_monitor** 고정 데이터베이스 역할의 멤버여야 합니다. 파트너 서버 인스턴스 중 하나에서만 **sysadmin** 또는 **dbm_monitor** 의 멤버인 경우 모니터는 해당 파트너에만 연결될 수 있습니다. 즉, 모니터는 다른 파트너에서 정보를 검색할 수 없습니다. 자세한 내용은 [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md)을 참조하세요.  
  
## <a name="menu-options"></a>메뉴 옵션  
 SQL Server 모니터에는 SQL Server 모니터와 관련된 명령을 포함하는 메뉴가 있습니다. 또한 이 메뉴에는 선택한 모듈의 명령이 포함될 수 있습니다.  
  
 SQL Server 모니터와 관련된 메뉴 옵션은 다음과 같습니다.  
  
 **최근에 사용한 파일**  
 이 메뉴는 **종료** 명령을 포함합니다.  
  
 **동작**  
 탐색 트리에서 선택한 노드의 상황에 맞는 메뉴를 포함합니다.  
  
 **Go**  
 모니터링 구성 요소의 목록을 포함합니다.  
  
-   데이터베이스 미러링  
  
-   복제  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링을 모니터링하려면**  
  
-   [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
