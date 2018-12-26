---
title: 데이터베이스 미러링 및 데이터베이스 스냅숏(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- snapshots [SQL Server database snapshots], database mirroring
- database snapshots [SQL Server], database mirroring
ms.assetid: 0bf1be90-7ce4-484c-aaa7-f8a782f57c5f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3c643ad9a84c6afe5b6ff08fd6716753ef42f79e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131694"
---
# <a name="database-mirroring-and-database-snapshots-sql-server"></a>데이터베이스 미러링 및 데이터베이스 스냅숏(SQL Server)
  가용성 목적으로 유지 관리 중인 미러 데이터베이스를 활용하여 보고 작업을 오프로드할 수 있습니다. 미러 데이터베이스를 보고 용도로 사용하려면 미러 데이터베이스에서 데이터베이스 스냅숏을 만들고 클라이언트 연결 요청을 가장 최근의 스냅숏으로 지정할 수 있습니다. 데이터베이스 스냅숏은 스냅숏이 만들어진 시점에 존재하던 원본 데이터베이스의 정적, 읽기 전용, 트랜잭션 일치 스냅숏입니다. 미러 데이터베이스에서 데이터베이스 스냅숏을 만들려면 데이터베이스가 동기화된 미러링 상태여야 합니다.  
  
 미러 데이터베이스와 달리 데이터베이스 스냅숏은 클라이언트에서 액세스할 수 있습니다. 미러 서버가 주 서버와 통신하고 있는 한, 보고 클라이언트를 스냅숏에 연결하도록 지시할 수 있습니다. 데이터베이스 스냅숏은 정적이기 때문에 새로운 데이터를 사용할 수 없습니다. 사용자가 비교적 최근 데이터를 사용하려면 정기적으로 새 데이터베이스 스냅숏을 만들고 애플리케이션에서 들어오는 클라이언트 연결을 최신 스냅숏으로 지정하도록 해야 합니다.  
  
 새 데이터베이스 스냅숏은 거의 비어 있지만 시간이 경과하면서 점점 더 많은 데이터베이스 페이지가 처음으로 업데이트됨에 따라 확장됩니다. 데이터베이스의 모든 스냅숏이 이렇게 증분 방식으로 증가하기 때문에 각 데이터베이스 스냅숏에서 일반 데이터베이스만큼 많은 리소스를 사용합니다. 미러 서버와 주 서버의 구성에 따라 미러 데이터베이스에 있는 데이터베이스 스냅숏의 수가 너무 많으면 주 데이터베이스의 성능이 느려질 수 있으므로 몇 개의 최근 스냅숏만 미러 데이터베이스에 보관하는 것이 좋습니다. 대체 스냅숏을 만든 후 들어오는 쿼리를 새 스냅숏으로 리디렉션하고 현재 쿼리가 완료된 후에는 이전 스냅숏을 삭제해야 합니다.  
  
> [!NOTE]  
>  데이터베이스 스냅숏에 대한 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.  
  
 역할이 전환되면 데이터베이스와 해당 스냅숏이 다시 시작되고 일시적으로 사용자와의 연결을 끊습니다. 그런 후 데이터베이스 스냅숏은 자신이 만들어진 서버 인스턴스에서 새로운 주 데이터베이스가 되어 그대로 유지됩니다. 사용자는 장애 조치(Failover) 후에도 스냅숏을 계속 사용할 수 있습니다. 그러나 이렇게 하면 새로운 주 서버에 추가 로드가 발생합니다. 환경에서 성능이 중요한 경우 새 미러 데이터베이스를 사용할 수 있게 되면 스냅숏을 만들어 클라이언트를 새 스냅숏으로 리디렉션하고 이전 미러 데이터베이스에서 모든 데이터베이스 스냅숏을 삭제하는 것이 좋습니다.  
  
> [!NOTE]  
>  확장이 용이한 전용 보고 솔루션의 경우에는 복제하십시오. 자세한 내용은 [SQL Server Replication](../install-windows/install-sql-server-replication.md)을(를) 참조하세요.  
  
## <a name="example"></a>예제  
 이 예에서는 미러된 데이터베이스의 스냅숏을 만듭니다.  
  
 데이터베이스 미러링 세션에 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]데이터베이스가 있다고 가정합니다. 이 예에서는 `AdventureWorks` 드라이브에 있는 `F` 데이터베이스의 미러 복사본에 대해 3개의 데이터베이스 스냅숏을 만듭니다. 스냅숏의 이름은 대략적인 생성 시간에 따라 각각 `AdventureWorks_0600`, `AdventureWorks_1200`및 `AdventureWorks_1800` 으로 지정됩니다.  
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]미러의 첫 번째 데이터베이스 스냅숏을 만듭니다.  
  
    ```  
    CREATE DATABASE AdventureWorks_0600  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_0600.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
2.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]미러의 두 번째 데이터베이스 스냅숏을 만듭니다. `AdventureWorks_0600` 사용자는 계속 사용할 수 있습니다.  
  
    ```  
    CREATE DATABASE AdventureWorks_1200  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1200.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     이 시점에서 프로그래밍 방식으로 새 클라이언트 연결을 최신 스냅숏으로 지정할 수 있습니다.  
  
3.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]미러의 세 번째 스냅숏을 만듭니다. `AdventureWorks_0600` 또는 `AdventureWorks_1200` 사용자는 계속 사용할 수 있습니다.  
  
    ```  
    CREATE DATABASE AdventureWorks_1800  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1800.SNP')  
        AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     이 시점에서 프로그래밍 방식으로 새 클라이언트 연결을 최신 스냅숏으로 지정할 수 있습니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 스냅숏 만들기&#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [데이터베이스 스냅숏 보기&#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [데이터베이스 스냅숏 삭제&#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  

  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [데이터베이스 미러링 세션에 클라이언트 연결&#40;SQL Server&#41;](connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  
