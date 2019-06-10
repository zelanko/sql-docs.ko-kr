---
title: Windows 인증을 사용하여 데이터베이스 미러링 모니터 서버 추가(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], establishing
- Windows authentication [SQL Server]
- database mirroring [SQL Server], witness
ms.assetid: bf5e87df-91a4-49f9-ae88-2a6dcf644510
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 97d7daf07250f60859f73c15874a0a6dfb7a4cbc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66775024"
---
# <a name="add-a-database-mirroring-witness-using-windows-authentication-transact-sql"></a>Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  데이터베이스에 미러링 모니터를 설정하려면 데이터베이스 소유자는 데이터베이스 엔진 인스턴스를 미러링 모니터 서버의 역할로 할당해야 합니다. 미러링 모니터 서버 인스턴스는 주 서버 인스턴스 또는 미러 서버 인스턴스와 동일한 컴퓨터에서 실행될 수 있으나 이 경우 자동 장애 조치(Failover)의 효과가 크게 저하됩니다.  
  
 그러므로 미러링 모니터를 동일한 컴퓨터에서 사용하지 않는 것이 좋습니다. 지정된 서버는 같은 파트너 또는 다른 파트너에 있는 여러 개의 동시 데이터베이스 미러링 세션에 참여할 수 있습니다. 지정된 서버는 한 세션에서는 파트너가 되고, 다른 세션에서는 미러링 모니터가 될 수 있습니다.  
  
 미러링 모니터는 자동 장애 조치가 있는 보호 우선 모드에만 사용됩니다. 미러링 모니터를 설정하기 전에 현재 SAFETY 속성이 FULL로 설정되어 있는지 확인합니다.  
  
> [!IMPORTANT]  
>  구성이 성능에 영향을 줄 수 있으므로 사용률이 낮은 시간에 데이터베이스 미러링을 구성하는 것이 좋습니다.  
  
### <a name="to-establish-a-witness"></a>미러링 모니터를 설정하려면  
  
1.  미러링 모니터 서버 인스턴스에 데이터베이스 미러링을 위한 하나의 엔드포인트가 있는지 확인합니다. 지원할 미러링 세션 수에 관계없이 서버 인스턴스는 데이터베이스 미러링 엔드포인트가 하나만 있어야 합니다. 데이터베이스 미러링 세션에서 이 서버 인스턴스를 미러링 모니터로만 사용하려면 미러링 모니터의 역할을 엔드포인트에 할당합니다(ROLE **=** WITNESS). 이 서버 인스턴스를 하나 이상의 다른 데이터베이스 미러링 세션에서 파트너로 사용하려면 엔드포인트의 역할을 ALL로 할당합니다.  
  
     SET WITNESS 문을 실행하려면 파트너 간에 데이터베이스 미러링 세션이 시작되어 있고 미러링 모니터 엔드포인트의 STATE가 STARTED로 설정되어 있어야 합니다.  
  
     미러링 모니터 서버 인스턴스에 데이터베이스 미러링 엔드포인트가 있는지 여부와 해당 인스턴스에서의 역할 및 상태를 확인하려면 다음 Transact-SQL 문을 사용하세요.  
  
    ```  
    SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
    > [!IMPORTANT]  
    >  데이터베이스 미러링 엔드포인트가 있으며 이미 사용 중인 경우 서버 인스턴스의 모든 세션에 이 엔드포인트를 사용하는 것이 좋습니다. 사용 중인 엔드포인트를 삭제하면 기존 세션의 연결이 손상됩니다. 세션에 미러링 모니터가 설정된 경우 데이터베이스 미러링 엔드포인트를 삭제하면 해당 세션의 주 서버에서 쿼럼이 손실될 수 있습니다. 이 경우 데이터베이스는 오프라인 상태가 되며 해당 사용자의 연결이 끊어집니다. 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
     미러링 모니터 서버에 엔드포인트가 없는 경우 [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)을 참조하세요.  
  
2.  파트너 인스턴스가 여러 도메인 사용자 계정으로 실행되는 경우 각 인스턴스의 master 데이터베이스에서 여러 계정에 대한 로그인을 만듭니다. 자세한 내용은 [Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용 &40;SQL Server &#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)을 참조하세요.  
  
3.  주 서버에 연결하여 다음 문을 실행합니다.  
  
     ALTER DATABASE *<database_name>* SET WITNESS **=** _<server_network_address>_  
  
     여기서 *<database_name>* 은 미러링할 데이터베이스의 이름(두 파트너에서 이 이름은 동일함)이고 *<server_network_address>* 는 미러링 모니터 서버 인스턴스의 서버 네트워크 주소입니다.  
  
     서버 네트워크 주소 구문은 다음과 같습니다.  
  
     TCP<b>://</b> _\<system-address>_ <b>:</b> _\<port>_  
  
     여기서 \<*system-address&gt;* 는 대상 컴퓨터 시스템을 명확하게 식별하는 문자열이고, \<*포트&gt;* 는 파트너 서버 인스턴스의 미러링 엔드포인트에서 사용되는 포트 번호입니다. 자세햔 내용은 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)을 사용합니다.  
  
     예를 들어 주 서버 인스턴스에서 다음 ALTER DATABASE 문은 미러링 모니터를 설정합니다. 데이터베이스 이름은 **AdventureWorks**이고 시스템 주소는 DBSERVER3(미러링 모니터 시스템의 이름)이며 미러링 모니터의 데이터베이스 미러링 엔드포인트에 사용되는 포트는 `7022`입니다.  
  
    ```  
    ALTER DATABASE AdventureWorks   
      SET WITNESS = 'TCP://DBSERVER3:7022'  
    ```  
  
## <a name="example"></a>예제  
 다음 예에서는 데이터 미러링 모니터를 설정합니다. 미러링 모니터 서버 인스턴스( `WITNESSHOST4`의 기본 인스턴스)에서 다음을 수행하십시오.  
  
1.  포트 `7022`만 사용하여 WITNESS 역할에 대한 이 서버 인스턴스의 엔드포인트를 만듭니다.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=WITNESS)  
    GO  
    ```  
  
2.  서로 다른 경우 파트너 인스턴스의 도메인 사용자 계정에 대한 로그인을 만듭니다. 예를 들어 미러링 모니터는 `SOMEDOMAIN\witnessuser`로 실행되고 있고 파트너는 `MYDOMAIN\dbousername`으로 실행되고 있다고 가정합니다. 다음과 같이 파트너에 대한 로그인을 만드십시오.  
  
    ```  
    --Create a login for the partner server instances,  
    --which are both running as MYDOMAIN\dbousername:  
    USE master ;  
    GO  
    CREATE LOGIN [MYDOMAIN\dbousername] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account   
    --of partners  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [MYDOMAIN\dbousername];  
    GO  
    ```  
  
3.  각 파트너 서버 인스턴스에서 미러링 모니터 서버 인스턴스에 대한 로그인을 만듭니다.  
  
    ```  
    --Create a login for the witness server instance,  
    --which is running as SOMEDOMAIN\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [SOMEDOMAIN\witnessuser] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account   
    --of partners  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [SOMEDOMAIN\witnessuser];  
    GO  
    ```  
  
4.  주 서버에서 `WITNESSHOST4`에 있는 미러링 모니터를 설정합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET WITNESS =   
        'TCP://WITNESSHOST4:7022'  
    GO  
    ```  
  
> [!NOTE]  
>  서버 네트워크 주소는 포트 번호로 대상 서버 인스턴스를 나타내며, 대상 서버 인스턴스는 인스턴스의 미러링 엔드포인트로 매핑됩니다.  
  
 보안 설정 표시, 미러 데이터베이스 준비, 파트너 설정 및 미러링 모니터 서버 추가 등의 작업을 수행하는 전체 예제는 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용  &#40;SQL Server &#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)   
 [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기 &#40;Transact-SQL &#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)   
 [데이터베이스 미러링 세션에서 미러링 모니터 서버 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)   
 [데이터베이스 미러링 모니터 서버](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
