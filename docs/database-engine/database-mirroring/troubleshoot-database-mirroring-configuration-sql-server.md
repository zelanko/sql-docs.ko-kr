---
title: 데이터베이스 미러링 구성 문제 해결(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- endpoints [SQL Server], database mirroring
- database mirroring [SQL Server], troubleshooting
- troubleshooting [SQL Server], database mirroring
ms.assetid: 87d3801b-dc52-419e-9316-8b1f1490946c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 714481541ee0060759aff3533add80d04ceebc8b
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54257188"
---
# <a name="troubleshoot-database-mirroring-configuration-sql-server"></a>데이터베이스 미러링 구성 문제 해결(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 데이터베이스 미러링 세션을 설정할 때 발생하는 문제를 해결하는 데 도움이 되는 정보를 제공합니다.  
  
> [!NOTE]  
>  [데이터베이스 미러링을 위한 선행 조건](../../database-engine/database-mirroring/prerequisites-restrictions-and-recommendations-for-database-mirroring.md)을 모두 충족하는지 확인하세요.  
  
|문제점|요약|  
|-----------|-------------|  
|오류 메시지 1418|이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메시지는 서버 네트워크 주소가 없거나 도달할 수 없음을 나타내며 네트워크 주소 이름을 확인한 후 명령을 다시 실행하도록 제안합니다. |  
|[계정](#Accounts)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행되고 있는 계정을 올바르게 구성하기 위한 요구 사항에 대해 설명합니다.|  
|[엔드포인트](#Endpoints)|각 서버 인스턴스의 데이터베이스 미러링 엔드포인트를 올바르게 구성하기 위한 요구 사항에 대해 설명합니다.|  
|[SystemAddress](#SystemAddress)|데이터베이스 미러링 구성에서 서버 인스턴스의 시스템 이름을 지정하는 대체 방법을 요약합니다.|  
|[네트워크 액세스](#NetworkAccess)|각 서버 인스턴스에서 TCP를 통해 다른 서버 인스턴스의 포트에 액세스할 수 있어야 한다는 요구 사항에 대해 설명합니다.|  
|[미러 데이터베이스 준비](#MirrorDbPrep)|미러링이 시작될 수 있도록 미러 데이터베이스를 준비하기 위한 요구 사항을 요약합니다.|  
|[파일 생성 작업 실패](#FailedCreateFileOp)|파일 생성 작업이 실패할 경우의 대처 방법에 대해 설명합니다.|  
|[Transact-SQL을 사용하여 미러링 시작](#StartDbm)|ALTER DATABASE *database_name* SET PARTNER **='**_partner_server_**'** 문의 필요한 순서에 대해 설명합니다.|  
|[데이터베이스 간 트랜잭션](#CrossDbTxns)|자동 장애 조치(Failover)를 사용할 경우 미결 트랜잭션이 자동으로 잘못 해결될 수 있습니다. 이러한 이유로 데이터베이스 미러링은 데이터베이스 간 트랜잭션을 지원하지 않습니다.|  
  
##  <a name="Accounts"></a> 계정  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행하고 있는 계정이 올바르게 구성되어 있어야 합니다.  
  
1.  계정에 올바른 권한이 있어야 합니다.  
  
    1.  계정이 동일한 도메인 계정에서 실행되는 경우 잘못 구성할 가능성이 줄어듭니다.  
  
    2.  계정이 서로 다른 도메인에서 실행되거나 도메인 계정이 아닐 경우 다른 컴퓨터의 **master** 에 한 계정의 로그인을 만들고 엔드포인트에 대한 CONNECT 권한을 해당 로그인에 부여해야 합니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)을 참조하세요. 여기에는 네트워크 서비스 계정이 포함됩니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 로컬 시스템 계정을 사용하는 서비스로 실행되는 경우 인증서를 사용하여 인증해야 합니다. 자세한 내용은 [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)을 참조하세요.  
  
##  <a name="Endpoints"></a> 엔드포인트  
 엔드포인트를 올바르게 구성해야 합니다.  
  
1.  각 서버 인스턴스(주 서버, 미러 서버 및 미러링 모니터 서버)에는 데이터베이스 미러링 엔드포인트가 있어야 합니다. 자세한 내용은 [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md) 및 인증 형식에 따라 [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md) 또는 [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)을 참조하세요.  
  
2.  포트 번호가 정확한지 확인합니다.  
  
     서버 인스턴스의 데이터베이스 미러링 엔드포인트와 현재 연결된 포트를 식별하려면 [sys.database_mirroring_endpoints](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md) 및 [sys.tcp_endpoints](../../relational-databases/system-catalog-views/sys-tcp-endpoints-transact-sql.md) 카탈로그 뷰를 사용합니다.  
  
3.  설명하기 어려운 데이터베이스 미러링 설치 문제의 경우 각 서버 인스턴스를 조사하여 올바른 포트에서 수신하고 있는지 확인하는 것이 좋습니다.   
  
4.  엔드포인트가 시작되었는지 확인합니다(STATE=STARTED). 각 서버 인스턴스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    SELECT state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
     **state_desc** 열에 대한 자세한 내용은 [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)를 참조하세요.  
  
     엔드포인트를 시작하려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    ALTER ENDPOINT Endpoint_Mirroring   
    STATE = STARTED   
    AS TCP (LISTENER_PORT = <port_number>)  
    FOR database_mirroring (ROLE = ALL);  
    GO  
    ```  
  
     자세한 내용은 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)을 참조하세요.  
  
5.  ROLE이 정확한지 확인합니다. 각 서버 인스턴스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    SELECT role FROM sys.database_mirroring_endpoints;  
    GO  
    ```  
  
     자세한 내용은 [sys.database_mirroring_endpoints&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)를 참조하세요.  
  
6.  다른 서버 인스턴스에서 서비스 계정에 로그인하려면 CONNECT 권한이 필요합니다. 다른 서버에서 로그인할 경우 CONNECT 권한이 있는지 확인합니다. 엔드포인트에 대한 CONNECT 권한이 있는 사용자를 파악하려면 각 서버 인스턴스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    SELECT 'Metadata Check';  
    SELECT EP.name, SP.STATE,   
       CONVERT(nvarchar(38), suser_name(SP.grantor_principal_id))   
          AS GRANTOR,   
       SP.TYPE AS PERMISSION,  
       CONVERT(nvarchar(46),suser_name(SP.grantee_principal_id))   
          AS GRANTEE   
       FROM sys.server_permissions SP , sys.endpoints EP  
       WHERE SP.major_id = EP.endpoint_id  
       ORDER BY Permission,grantor, grantee;   
    GO  
  
    ```  
  
##  <a name="SystemAddress"></a> 시스템 주소  
 데이터베이스 미러링 구성에서 서버 인스턴스의 시스템 이름에는 시스템을 명확하게 식별하는 모든 이름을 사용할 수 있습니다. 서버 주소는 시스템 이름(시스템이 같은 도메인에 있는 경우), 정규화된 도메인 이름 또는 IP 주소(가급적 고정 IP 주소)일 수 있습니다. 정규화된 도메인 이름을 사용하는 것이 좋습니다. 자세햔 내용은 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)을 사용합니다.  
  
##  <a name="NetworkAccess"></a> Network Access  
 각 서버 인스턴스에서 TCP를 통해 다른 서버 인스턴스의 포트에 액세스할 수 있어야 합니다. 이는 서버 인스턴스가 서로 트러스트하지 않는 다른 도메인(트러스트되지 않은 도메인)에 있을 경우 특히 유용합니다. 이 경우 서버 인스턴스 간의 통신은 대부분 제한됩니다.  
  
##  <a name="MirrorDbPrep"></a> Mirror Database Preparation  
 처음으로 미러링을 시작하는 것이든 미러링을 제거한 후 다시 시작하는 것이든 관계없이 미러 데이터베이스가 미러링을 위한 준비를 완료했는지 확인합니다.  
  
 미러 서버에 미러 데이터베이스를 만들 때는 WITH NORECOVERY로 동일한 데이터베이스 이름을 지정하여 주 데이터베이스의 백업을 복원하도록 해야 합니다. 백업 후에 생성된 모든 로그 백업도 WITH NORECOVERY를 사용하여 적용해야 합니다.  
  
 또한 가능한 경우 드라이브 문자를 포함한 미러 데이터베이스의 파일 경로가 주 데이터베이스의 경로와 동일한 것이 좋습니다. 주 데이터베이스는 'F:' 드라이브에 있는데 미러 시스템에는 F: 드라이브가 없는 경우 등 파일 경로가 달라야 하는 경우에는 RESTORE 문에 MOVE 옵션을 포함해야 합니다.  
  
> [!IMPORTANT]  
>  미러 데이터베이스를 만들 때 데이터베이스 파일을 이동한 경우 나중에 데이터베이스에 파일을 추가하려면 미러링을 일시 중지해야 할 수도 있습니다.  
  
 데이터베이스 미러링이 중지된 경우 주 데이터베이스에서 수행된 모든 후속 로그 백업을 미러 데이터베이스에 적용해야만 미러링을 다시 시작할 수 있습니다.  
  
 자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)을 사용합니다.  
  
##  <a name="FailedCreateFileOp"></a> Failed Create-File Operation  
 미러링 세션에 영향을 주지 않고 파일을 추가하려면 파일의 경로가 두 서버 모두에 있어야 합니다. 따라서 미러 데이터베이스를 만들 때 데이터베이스 파일을 이동하면 나중에 미러 데이터베이스에 파일을 추가할 수 없고 미러링이 일시 중지될 수 있습니다.  
  
 이 문제를 해결하려면  
  
1.  데이터베이스 소유자가 미러링 세션을 제거하고 추가된 파일이 들어 있는 파일 그룹의 전체 백업을 복원해야 합니다.  
  
2.  그러 다음 소유자가 주 서버에서 파일 추가 작업이 포함된 로그를 백업하고 WITH NORECOVERY 및 WITH MOVE 옵션을 사용하여 미러 데이터베이스에 로그 백업을 수동으로 복원해야 합니다. 이렇게 하면 미러 서버에 지정된 파일 경로가 만들어지고 새 파일이 이 위치에 복원됩니다.  
  
3.  새 미러링 세션에 대비해서 데이터베이스를 준비하려면 소유자가 주 서버에서 WITH NO RECOVERY 및 기타 처리 중인 로그 백업도 복원해야 합니다.  
  
 자세한 내용은 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md), [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md), [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md), [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md) 또는 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)을 참조하세요.  
  
##  <a name="StartDbm"></a> Transact-SQL을 사용하여 미러링 시작  
 ALTER DATABASE *database_name* SET PARTNER **='**_partner_server_**'** 문을 실행하는 순서는 매우 중요합니다.  
  
1.  미러 서버에서 첫 번째 문을 실행해야 합니다. 이 문을 실행할 때는 미러 서버에서 다른 서버 인스턴스에 연결하지 않고 대신 주 서버가 미러 서버에 접속할 때까지 기다리도록 해당 데이터베이스에 지시합니다.  
  
2.  주 서버에서 두 번째 ALTER DATABASE 문을 실행해야 합니다. 이 문을 실행하면 주 서버가 미러 서버에 연결을 시도합니다. 이 연결이 생성되면 미러 서버는 다른 연결을 통해 주 서버에 연결을 시도합니다.  
  
 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 미러링을 시작하는 방법은 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)을 참조하세요.  
  
##  <a name="CrossDbTxns"></a> 데이터베이스 간 트랜잭션  
 자동 장애 조치(Failover) 있는 보호 우선 모드로 데이터베이스를 미러링하는 경우 자동 장애 조치로 인해 미결 트랜잭션이 자동으로 잘못 해결될 수 있습니다. 데이터베이스 간 트랜잭션을 커밋하는 동안 두 데이터베이스 중 하나에서 자동 장애 조치가 수행되면 데이터베이스 간에 논리적 불일치가 발생할 수 있습니다.  
  
 자동 장애 조치의 영향을 받을 수 있는 데이터베이스 간 트랜잭션 유형은 다음과 같습니다.  
  
-   동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 여러 데이터베이스를 업데이트하는 트랜잭션  
  
-   MS DTC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator)를 사용하는 트랜잭션  
  
 자세한 내용은 [Always On 가용성 그룹 및 데이터베이스 미러링에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)  
  
  


