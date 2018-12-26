---
title: 데이터베이스 미러링 - 세션 설정 - Windows 인증 | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 143c68a5-589f-4e7f-be59-02707e1a430a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9270b71457bdbb6e932015ddcad8118ef2f42cdd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529917"
---
# <a name="database-mirroring---establish-session---windows-authentication"></a>데이터베이스 미러링 - 세션 설정 - Windows 인증
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]을 대신 사용합니다.  
  
 미러 데이터베이스를 준비한 후( [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)참조) 데이터베이스 미러링 세션을 구성합니다. 주 서버, 미러 서버 및 미러링 모니터 서버 인스턴스는 다른 호스트 시스템에 있는 별도의 서버 인스턴스여야 합니다.  
  
> [!IMPORTANT]  
>  미러링 구성은 성능에 영향을 줄 수 있으므로 사용률이 낮은 시간에 데이터베이스 미러링을 구성하는 것이 좋습니다.  
  
> [!NOTE]  
>  지정된 서버 인스턴스는 같은 파트너 또는 다른 파트너에 있는 여러 개의 동시 데이터베이스 미러링 세션에 참여할 수 있습니다. 서버 인스턴스는 한 세션에서는 파트너가 되고, 다른 세션에서는 미러링 모니터 서버가 될 수 있습니다. 미러 서버 인스턴스는 주 서버 인스턴스와 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 실행해야 합니다. 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 데이터베이스 미러링을 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요. 또한 서버 인스턴스는 동일한 작업을 처리할 수 있는 동등한 시스템에서 실행하는 것이 좋습니다.  
  
### <a name="to-establish-a-database-mirroring-session"></a>데이터베이스 미러링 세션을 구성하려면  
  
1.  미러 데이터베이스를 만듭니다. 자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)버전에서는 데이터베이스 미러링을 사용할 수 없습니다.  
  
2.  각 서버 인스턴스에서 보안을 설정합니다.  
  
     데이터베이스 미러링 세션의 각 서버 인스턴스에는 데이터베이스 미러링 엔드포인트가 필요합니다. 따라서 엔드포인트가 없으면 만들어야 합니다.  
  
    > [!NOTE]  
    >  서버 인스턴스에서 데이터베이스 미러링에 사용하는 인증 형식은 데이터베이스 미러링 엔드포인트의 속성입니다. 데이터베이스 미러링에서 사용할 수 있는 두 가지 전송 보안 유형으로 Windows 인증과 인증서 기반 인증이 있습니다. 자세한 내용은 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)을 참조하세요.  
  
     각 파트너 서버에서 데이터베이스 미러링의 엔드포인트가 있는지 확인합니다. 지원할 미러링 세션의 수에 관계없이 서버 인스턴스에는 데이터베이스 미러링 엔드포인트가 하나만 있어야 합니다. 이 서버 인스턴스를 데이터베이스 미러링 세션의 파트너 전용으로 사용하려면 엔드포인트에 파트너 역할을 할당합니다(ROLE**=** PARTNER). 이 서버를 다른 데이터베이스 미러링 세션에서 미러링 모니터 서버로도 사용하려면 엔드포인트 역할을 ALL로 지정합니다.  
  
     SET PARTNER 문을 실행하려면 두 파트너의 엔드포인트에 대한 STATE가 STARTED로 설정되어 있어야 합니다.  
  
     서버 인스턴스에 데이터베이스 미러링 엔드포인트가 있는지 확인하고 그 역할과 상태를 확인하려면 해당 인스턴스에 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
    > [!IMPORTANT]  
    >  사용 중인 데이터베이스 미러링 엔드포인트는 다시 구성하지 마세요. 데이터베이스 미러링 엔드포인트가 있으며 이미 사용 중인 경우 서버 인스턴스의 모든 세션에 이 엔드포인트를 사용하는 것이 좋습니다. 사용 중인 엔드포인트를 삭제하면 엔드포인트가 다시 시작되어 기존 세션의 연결이 끊어지므로 다른 서버 인스턴스에서 오류가 발생할 수 있습니다. 이는 특히 파트너에 엔드포인트를 다시 구성하면 장애 조치(Failover) 오류가 발생할 수 있는 자동 장애 조치(Failover)가 있는 보호 우선 모드에서 중요한 사항입니다. 또한 세션에 미러링 모니터 서버가 설정된 경우 데이터베이스 미러링 엔드포인트를 삭제하면 해당 세션의 주 서버에서 쿼럼이 손실될 수 있습니다. 이 경우 데이터베이스는 오프라인 상태가 되며 해당 사용자의 연결이 끊어집니다. 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
     파트너 중 하나에 엔드포인트가 없는 경우 [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기 &#40;Transact-SQL &#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)버전에서는 데이터베이스 미러링을 사용할 수 없습니다.  
  
3.  서버 인스턴스가 여러 도메인 사용자 계정으로 실행되는 경우 각 인스턴스는 다른 인스턴스의 **master** 데이터베이스에서 로그인을 필요로 합니다. 따라서 로그인이 없으면 만들어야 합니다. 자세한 내용은 [Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용 &#40;SQL Server &#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)을 참조하세요.  
  
4.  미러 데이터베이스에서 주 서버를 파트너로 설정하려면 미러 서버에 연결하여 다음 문을 실행합니다.  
  
     ALTER DATABASE *\<database_name\>* SET PARTNER **=**_\<server\_network\_address\>_  
  
     여기서 _\<database\_name\>_ 은 미러링할 데이터베이스의 이름(두 파트너에서 이 이름은 동일함)이고 _\<server\_network\_address\>_ 는 주 서버의 서버 네트워크 주소입니다.  
  
     서버 네트워크 주소 구문은 다음과 같습니다.  
  
     TCP<b>\://</b>_\<system-address\>_<b>\:</b>_\<port\>_  
  
     여기서 _\<system-address&gt;_ 는 대상 컴퓨터 시스템을 명확하게 식별하는 문자열이고, _\<포트&gt;_ 는 파트너 서버 인스턴스의 미러링 엔드포인트에서 사용되는 포트 번호입니다. 자세햔 내용은 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)을 사용합니다.  
  
     예를 들어 미러 서버 인스턴스에서 다음 ALTER DATABASE 문은 파트너를 원래 주 서버 인스턴스로 설정합니다. 데이터베이스 이름은 **AdventureWorks**이고 시스템 주소는 DBSERVER1(파트너 시스템의 이름)이며 파트너의 데이터베이스 미러링 엔드포인트에서 사용되는 포트는 7022입니다.  
  
    ```  
    ALTER DATABASE AdventureWorks   
       SET PARTNER = 'TCP://DBSERVER1:7022'  
    ```  
  
     이 문은 주 서버에서 접속할 때 세션을 구성하도록 미러 서버를 준비합니다.  
  
5.  주 데이터베이스에서 미러 서버를 파트너로 설정하려면 주 서버에 연결하여 다음 문을 실행합니다.  
  
     ALTER DATABASE _\<database\_name\>_ SET PARTNER **=**_\<server\_network\_address\>_  
  
     자세한 내용은 4단계를 참조하십시오.  
  
     예를 들어 주 서버 인스턴스에서 다음 ALTER DATABASE 문은 파트너를 원래 미러 서버 인스턴스로 설정합니다. 데이터베이스 이름은 **AdventureWorks**이고 시스템 주소는 DBSERVER2(파트너 시스템의 이름)이며 파트너의 데이터베이스 미러링 엔드포인트에서 사용되는 포트는 7025입니다.  
  
    ```  
    ALTER DATABASE AdventureWorks SET PARTNER = 'TCP://DBSERVER2:7022'  
    ```  
  
     주 서버에서 이 문을 입력하면 데이터베이스 미러링 세션이 시작됩니다.  
  
6.  기본적으로 세션은 전체 트랜잭션 보안으로 설정되므로(SAFETY가 FULL로 설정됨) 자동 장애 조치를 지원하지 않는 동기 보호 우선 모드로 세션이 시작됩니다. 이러한 세션을 다음과 같이 자동 장애 조치(Failover)가 있는 보호 우선 모드나 비동기 성능 우선 모드에서 실행되도록 다시 구성할 수 있습니다.  
  
    -   **자동 장애 조치 있는 보호 우선 모드**  
  
         자동 장애 조치(Failover)가 있는 보호 우선 모드로 세션을 실행하려면 미러링 모니터 서버 인스턴스를 추가합니다. 자세한 내용은 [Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)를 참조하세요.  
  
    -   **성능 우선 모드**  
  
         자동 장애 조치 기능을 지원하지 않고 가용성보다 성능을 우선하려면 트랜잭션 보안을 해제합니다. 자세한 내용은 [데이터베이스 미러링 세션에서 트랜잭션 보안 변경&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)을 참조하세요.  
  
        > [!NOTE]  
        >  성능 우선 모드에서는 WITNESS를 OFF로 설정해야 합니다. 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
## <a name="example"></a>예제  
  
> [!NOTE]  
>  다음 예에서는 기존 미러 데이터베이스의 파트너 간에 데이터베이스 미러링 세션을 설정합니다. 미러 데이터베이스를 만드는 방법은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)를 참조하세요.  
  
 이 예에서는 미러링 모니터 서버 없이 데이터베이스 미러링 세션을 만드는 기본 단계를 보여 줍니다. 두 파트너는 두 컴퓨터 시스템(PARTNERHOST1 및 PARTNERHOST5)의 기본 서버 인스턴스입니다. 두 파트너 인스턴스는 동일한 Windows 도메인 사용자 계정(MYDOMAIN\dbousername)을 실행합니다.  
  
1.  주 서버 인스턴스(PARTNERHOST1의 기본 인스턴스)에서 포트 7022를 사용하여 모든 역할을 지원하는 엔드포인트를 만듭니다.  
  
    ```  
    --create an endpoint for this instance  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    ```  
  
    > [!NOTE]  
    >  로그인을 설정하는 방법의 예제는 [Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용 &#40;SQL Server &#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)버전에서는 데이터베이스 미러링을 사용할 수 없습니다.  
  
2.  미러 서버 인스턴스(PARTNERHOST5의 기본 인스턴스)에서 포트 7022를 사용하여 모든 역할을 지원하는 엔드포인트를 만듭니다.  
  
    ```  
    --create an endpoint for this instance  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    ```  
  
3.  PARTNERHOST1의 주 서버 인스턴스에서 데이터베이스를 백업합니다.  
  
    ```  
    BACKUP DATABASE AdventureWorks   
        TO DISK = 'C:\AdvWorks_dbmirror.bak'   
        WITH FORMAT  
    GO  
    ```  
  
4.  `PARTNERHOST5`의 미러 서버 인스턴스에서 데이터베이스를 복원합니다.  
  
    ```  
    RESTORE DATABASE AdventureWorks   
        FROM DISK = 'Z:\AdvWorks_dbmirror.bak'   
        WITH NORECOVERY  
    GO  
    ```  
  
5.  전체 데이터베이스 백업을 만든 후 주 데이터베이스에서 로그 백업을 만들어야 합니다. 예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 앞의 데이터베이스 백업에 사용된 동일한 파일에 로그를 백업합니다.  
  
    ```  
    BACKUP LOG AdventureWorks   
        TO DISK = 'C:\AdventureWorks.bak'   
    GO  
    ```  
  
6.  미러링을 시작하기 전에 필수 로그 백업 및 모든 후속 로그 백업을 적용해야 합니다.  
  
     예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 C:\AdventureWorks.bak로부터 첫 번째 로그를 복원합니다.  
  
    ```  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\ AdventureWorks.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  미러 서버 인스턴스에서 PARTNERHOST1의 서버 인스턴스를 파트너로 설정하여 초기 주 서버로 만듭니다.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks   
        SET PARTNER =   
        'TCP://PARTNERHOST1:7022'  
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  기본적으로 데이터베이스 미러링 세션은 전체 트랜잭션 보안(SAFETY가 FULL로 설정됨)에 따라 달라지는 동기 모드로 실행됩니다. 비동기 성능 우선 모드로 세션을 실행하려면 SAFETY를 OFF로 설정합니다. 자세한 내용은 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)을 참조하세요.  
  
8.  주 서버 인스턴스에서 `PARTNERHOST5` 의 서버 인스턴스를 파트너로 설정하여 초기 미러 서버로 만듭니다.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://PARTNERHOST5:7022'  
    GO  
    ```  
  
9. 필요에 따라 자동 장애 조치(Failover)가 있는 보호 우선 모드를 사용하려면 미러링 모니터 서버 인스턴스를 설정합니다. 자세한 내용은 [Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
>  보안 설정 표시, 미러 데이터베이스 준비, 파트너 설정 및 미러링 모니터 서버 추가 등의 작업을 수행하는 전체 예제는 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용 &#40;SQL Server &#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)   
 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기 &#40;Transact-SQL &#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [데이터베이스 미러링 및 로그 전달&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)   
 [데이터베이스 미러링 운영 모드](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  

