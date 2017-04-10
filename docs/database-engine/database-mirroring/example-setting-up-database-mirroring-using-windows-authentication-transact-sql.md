---
title: "예제: Windows 인증을 사용하여 데이터베이스 미러링 설정(Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터베이스 미러링 [SQL Server], 배포"
  - "Windows 인증 [SQL Server]"
  - "인증 [SQL Server], 데이터베이스 미러링"
  - "데이터베이스 미러링 [SQL Server], 보안"
ms.assetid: 35800769-aede-4aac-b077-0e0e487e302f
caps.latest.revision: 41
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 41
---
# 예제: Windows 인증을 사용하여 데이터베이스 미러링 설정(Transact-SQL)
  이 예에서는 Windows 인증을 사용하는 미러링 모니터 서버가 있는 데이터베이스 미러링 세션을 만드는 데 필요한 모든 단계를 보여 줍니다. 이 항목의 예에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 단계를 사용하는 대신 데이터베이스 미러링 보안 구성 마법사를 데이터베이스 미러링 설치에 사용할 수도 있습니다. 자세한 내용은 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md)을 참조하세요.  
  
## 필수 구성 요소  
 예에서는 기본적으로 단순 복구 모델을 사용하는 **AdventureWorks** 예제 데이터베이스를 사용합니다. 데이터베이스 미러링을 이 데이터베이스에 사용하려면 전체 복구 모델을 사용하도록 변경해야 합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 복구 모델을 변경하려면 다음과 같이 ALTER DATABASE 문을 사용하십시오.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks   
SET RECOVERY FULL;  
GO  
```  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 복구 모델을 변경하는 방법에 대한 자세한 내용은 [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)을 참조하세요.  
  
### 사용 권한  
 데이터베이스에 대한 ALTER 권한과 CREATE ENDPOINT 권한 또는 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## 예제  
 이 예에서는 파트너 2개와 미러링 모니터 서버가 컴퓨터 시스템 3대의 기본 서버 인스턴스입니다. 3개의 서버 인스턴스에서는 같은 Windows 도메인을 실행하지만 예에 나오는 미러링 모니터 서버 인스턴스에는 다른 사용자 계정(시작 서비스 계정으로 사용)이 사용됩니다.  
  
 다음 표에서는 이 예에 사용된 값을 요약합니다.  
  
|초기 미러링 역할|호스트 시스템|도메인 사용자 계정|  
|----------------------------|-----------------|-------------------------|  
|주 서버|PARTNERHOST1|*\<Mydomain>\\<dbousername\>*|  
|미러|PARTNERHOST5|*\<Mydomain>\\<dbousername\>*|  
|미러링 모니터|WITNESSHOST4|*\<Somedomain>\\<witnessuser\>*|  
  
1.  주 서버 인스턴스(PARTNERHOST1의 기본 인스턴스)에 끝점을 만듭니다.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=PARTNER)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    -- Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
2.  미러 서버 인스턴스(PARTNERHOST5의 기본 인스턴스)에 끝점을 만듭니다.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
3.  미러링 모니터 서버 인스턴스(WITNESSHOST4의 기본 인스턴스)에 끝점을 만듭니다.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=WITNESS)  
    GO  
    --Create a login for the partner server instances,  
    --which are both running as Mydomain\dbousername:  
    USE master ;  
    GO  
    CREATE LOGIN [Mydomain\dbousername] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
4.  미러 데이터베이스를 만듭니다. 자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)를 참조하세요.  
  
5.  PARTNERHOST5의 미러 서버 인스턴스에서 PARTNERHOST1의 서버 인스턴스를 초기 주 서버 인스턴스로 만들어 파트너로 설정합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER =   
        'TCP://PARTNERHOST1.COM:7022'  
    GO  
    ```  
  
6.  PARTNERHOST1의 주 서버 인스턴스에서 PARTNERHOST5의 서버 인스턴스를 초기 미러 서버 인스턴스로 만들어 파트너로 설정합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://PARTNERHOST5.COM:7022'  
    GO  
    ```  
  
7.  주 서버에서 WITNESSHOST4에 있는 미러링 모니터 서버를 설정합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET WITNESS =   
        'TCP://WITNESSHOST4.COM:7022'  
    GO  
    ```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start the configuring database mirroring security wizard.md)  
  
-   [Trustworthy 속성을 사용하도록 미러 데이터베이스 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
-   [데이터베이스 미러링 끝점의 아웃바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database mirroring - use certificates for outbound connections.md)  
  
-   [데이터베이스 미러링 끝점의 인바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database mirroring - use certificates for inbound connections.md)  
  
-   [예제: 인증서를 사용하여 데이터베이스 미러링 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## 참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [데이터베이스 미러링 끝점&#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport security - database mirroring - always on availability.md)   
 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md)   
 [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  