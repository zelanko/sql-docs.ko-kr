---
title: '예제: 인증서를 사용하여 데이터베이스 미러링 설정(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: df489ecd-deee-465c-a26a-6d1bef6d7b66
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ea87e2de984107c5a0fda6eb2629ee5cfd197841
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934189"
---
# <a name="example-setting-up-database-mirroring-using-certificates-transact-sql"></a>예: 인증서를 사용하여 데이터베이스 미러링 설정(Transact-SQL)
  이 예에서는 인증서 기반 인증을 사용하여 데이터베이스 미러링 세션을 만드는 데 필요한 모든 단계를 보여 줍니다. 이 항목의 예에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용합니다. 네트워크 보안을 보장할 수 없는 경우 데이터베이스 미러링 연결에 암호화를 사용하는 것이 좋습니다.  
  
 인증서를 다른 시스템으로 복사할 때는 안전한 복사 방법을 사용하세요. 모든 인증서를 안전하게 보관하는 데 많은 주의를 기울여야 합니다.  
  
##  <a name="example"></a><a name="ExampleH2"></a> 예  
 다음 예에서는 HOST_A에 있는 한 파트너에서 실행되어야 하는 단계를 보여 줍니다. 이 예에서 파트너 2개는 컴퓨터 시스템 3대의 기본 서버 인스턴스입니다. 이 중 두 서버 인스턴스는 트러스트되지 않은 Windows 도메인에서 실행되므로 인증서 기반 인증이 필요합니다.  
  
 HOST_A는 초기 주 역할을 맡고 HOST_B는 미러 역할을 맡습니다.  
  
 인증서를 사용하여 데이터베이스 미러링을 설정하는 작업은 4개의 일반적인 단계로 이루어지며, 이 예제에서는 이 중 3개, 즉 1, 2, 4단계를 보여 줍니다. 이러한 단계는 다음과 같습니다.  
  
1.  [아웃바운드 연결 구성](#ConfiguringOutboundConnections)  
  
     이 예에서는 다음 작업을 위한 단계를 보여 줍니다.  
  
    1.  아웃바운드 연결에 대한 Host_A 구성  
  
    2.  아웃바운드 연결에 대한 Host_B 구성  
  
     이 데이터베이스 미러링 설정 단계에 대한 자세한 내용은 [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)을 사용합니다.  
  
2.  [인바운드 연결 구성](#ConfigureInboundConnections)  
  
     이 예에서는 다음 작업을 위한 단계를 보여 줍니다.  
  
    1.  인바운드 연결에 대한 Host_A 구성  
  
    2.  인바운드 연결에 대한 Host_B 구성  
  
     이 데이터베이스 미러링 설정 단계에 대한 자세한 내용은 [데이터베이스 미러링 엔드포인트의 인바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)을 사용합니다.  
  
3.  미러 데이터베이스 만들기  
  
     미러 데이터베이스를 만드는 방법에 대한 자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)을 사용합니다.  
  
4.  [미러링 파트너 구성](#ConfigureMirroringPartners)  
  
###  <a name="configuring-outbound-connections"></a><a name="ConfiguringOutboundConnections"></a>아웃 바운드 연결 구성  
 **아웃바운드 연결에 대한 Host_A를 구성하려면**  
  
1.  필요한 경우 master 데이터베이스에 데이터베이스 마스터 키를 만듭니다.  
  
    ```  
    USE master;  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<1_Strong_Password!>';  
    GO  
    ```  
  
2.  이 서버 인스턴스에 대한 인증서를 만듭니다.  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_A_cert   
       WITH SUBJECT = 'HOST_A certificate';  
    GO  
    ```  
  
3.  인증서를 사용하여 서버 인스턴스에 대한 미러링 엔드포인트를 만듭니다.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_A_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
4.  HOST_A 인증서를 백업하여 HOST_B 시스템에 복사합니다.  
  
    ```  
    BACKUP CERTIFICATE HOST_A_cert TO FILE = 'C:\HOST_A_cert.cer';  
    GO  
    ```  
  
5.  안전한 복사 방법을 사용하여 C:\HOST_A_cert.cer을 HOST_B로 복사합니다.  
  
 **아웃바운드 연결에 대한 Host_B를 구성하려면**  
  
1.  필요한 경우 master 데이터베이스에 데이터베이스 마스터 키를 만듭니다.  
  
    ```  
    USE master;  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Strong_Password_#2>';  
    GO  
    ```  
  
2.  HOST_B 서버 인스턴스에 대한 인증서를 만듭니다.  
  
    ```  
    CREATE CERTIFICATE HOST_B_cert   
       WITH SUBJECT = 'HOST_B certificate for database mirroring';  
    GO  
    ```  
  
3.  HOST_B 서버 인스턴스에 대한 미러링 엔드포인트를 만듭니다.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_B_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
4.  HOST_B 인증서를 백업합니다.  
  
    ```  
    BACKUP CERTIFICATE HOST_B_cert TO FILE = 'C:\HOST_B_cert.cer';  
    GO   
    ```  
  
5.  안전한 복사 방법을 사용하여 C:\HOST_B_cert.cer을 HOST_A로 복사합니다.  
  
 자세햔 내용은 [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)을 참조하세요.  
  
###  <a name="configuring-inbound-connections"></a><a name="ConfigureInboundConnections"></a>인바운드 연결 구성  
 **인바운드 연결에 대한 Host_A를 구성하려면**  
  
1.  HOST_A에서 HOST_B에 대한 로그인을 만듭니다.  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_B_login WITH PASSWORD = '1Sample_Strong_Password!@#';  
    GO  
    ```  
  
2.  --해당 로그인의 사용자를 만듭니다.  
  
    ```  
    CREATE USER HOST_B_user FOR LOGIN HOST_B_login;  
    GO  
    ```  
  
3.  --인증서를 사용자와 연결합니다.  
  
    ```  
    CREATE CERTIFICATE HOST_B_cert  
       AUTHORIZATION HOST_B_user  
       FROM FILE = 'C:\HOST_B_cert.cer'  
    GO  
    ```  
  
4.  해당 원격 미러링 엔드포인트에 대한 로그인에 CONNECT 권한을 부여합니다.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_B_login];  
    GO  
    ```  
  
 **인바운드 연결에 대한 Host_B를 구성하려면**  
  
1.  HOST_B에서 HOST_A에 대한 로그인을 만듭니다.  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_A_login WITH PASSWORD = '=Sample#2_Strong_Password2';  
    GO  
    ```  
  
2.  해당 로그인의 사용자를 만듭니다.  
  
    ```  
    CREATE USER HOST_A_user FOR LOGIN HOST_A_login;  
    GO  
    ```  
  
3.  인증서를 사용자와 연결합니다.  
  
    ```  
    CREATE CERTIFICATE HOST_A_cert  
       AUTHORIZATION HOST_A_user  
       FROM FILE = 'C:\HOST_A_cert.cer'  
    GO  
    ```  
  
4.  해당 원격 미러링 엔드포인트에 대한 로그인에 CONNECT 권한을 부여합니다.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_A_login];  
    GO  
    ```  
  
> [!IMPORTANT]  
>  자동 장애 조치(Failover)를 지원하는 보호 우선 모드에서 실행하려는 경우 아웃바운드 및 인바운드 연결에 대한 미러링 모니터를 구성하기 위해 같은 설정 단계를 반복해야 합니다. 미러링 모니터를 사용하는 경우 인바운드 연결을 설정하려면 두 파트너 모두에서 미러링 모니터에 대해 그리고 미러링 모니터에서 두 파트너 모두에 대해 로그인과 사용자를 설정해야 합니다.  
  
 자세햔 내용은 [데이터베이스 미러링 엔드포인트의 인바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)을 참조하세요.  
  
### <a name="creating-the-mirror-database"></a>미러 데이터베이스 만들기  
 미러 데이터베이스를 만드는 방법에 대한 자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)을 사용합니다.  
  
###  <a name="configuring-the-mirroring-partners"></a><a name="ConfigureMirroringPartners"></a>미러링 파트너 구성  
  
1.  HOST_B의 미러 서버 인스턴스에서 HOST_A의 서버 인스턴스를 초기 주 서버 인스턴스로 만들어 파트너로 설정합니다. `TCP://HOST_A.Mydomain.Corp.Adventure-Works``.com:7024`를 유효한 네트워크 주소로 대체합니다. 자세햔 내용은 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](specify-a-server-network-address-database-mirroring.md)을 사용합니다.  
  
    ```  
    --At HOST_B, set server instance on HOST_A as partner (principal server):  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://HOST_A.Mydomain.Corp.Adventure-Works.com:7024';  
    GO  
    ```  
  
2.  HOST_A의 주 서버 인스턴스에서 HOST_B의 서버 인스턴스를 초기 미러 서버 인스턴스로 만들어 파트너로 설정합니다. `TCP://HOST_B.Mydomain.Corp.Adventure-Works.com:7024`를 유효한 네트워크 주소로 대체합니다.  
  
    ```  
    --At HOST_A, set server instance on HOST_B as partner (mirror server).  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://HOST_B.Mydomain.Corp.Adventure-Works.com:7024';  
    GO  
    ```  
  
3.  이 예에서는 세션이 고성능 모드에서 실행될 것으로 가정합니다. 고성능 모드에 맞게 이 세션을 구성하려면 HOST_A의 주 서버 인스턴스에서 트랜잭션 보안을 OFF로 설정합니다.  
  
    ```  
    --Change to high-performance mode by turning off transacton safety.  
    ALTER DATABASE AdventureWorks   
        SET PARTNER SAFETY OFF  
    GO  
    ```  
  
    > [!NOTE]  
    >  자동 장애 조치 (failover)가 있는 보호 우선 모드에서 실행 하려면 트랜잭션 보안을 FULL (기본 설정)으로 설정 된 채로 두고 두 번째 set PARTNER **' *`partner_server`* '** 문을 실행 한 후 가능한 한 빨리 미러링 모니터 서버를 추가 합니다. 먼저 아웃바운드 및 인바운드 연결에 대한 미러링 모니터를 구성해야 합니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [데이터베이스 미러링 엔드포인트의 인바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [역할 전환 후 로그인 및 작업 관리&#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
-   [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)(SQL Server)  
  
-   [데이터베이스 미러링 구성 문제 해결&#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 및 AlwaysOn 가용성 그룹 &#40;SQL Server에 대 한 전송 보안&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [데이터베이스 미러링 &#40;서버 네트워크 주소를 지정&#41;](specify-a-server-network-address-database-mirroring.md)   
 [데이터베이스 미러링 끝점은 SQL Server을 &#40;&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Transact-sql&#41;&#40;데이터베이스 미러링 끝점에 대 한 인증서 사용](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL &#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [SQL Server 데이터베이스 엔진 및 Azure SQL Database 보안 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
