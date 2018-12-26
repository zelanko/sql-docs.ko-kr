---
title: 데이터베이스 미러링 - 인바운드 연결에 대한 인증서 사용 | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- certificates [SQL Server], database mirroring
- inbound connections
- database mirroring [SQL Server], security
ms.assetid: 5d48bb98-61f0-4b99-8f1a-b53f831d63d0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6057c87d7fb4e1a5f4b29879179efa0ff716275e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529688"
---
# <a name="database-mirroring---use-certificates-for-inbound-connections"></a>데이터베이스 미러링 - 인바운드 연결에 대한 인증서 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 인증서를 사용하여 데이터베이스 미러링의 인바운드 연결을 인증하도록 서버 인스턴스를 구성하는 단계에 대해 설명합니다. 인바운드 연결을 설정하려면 먼저 각 서버 인스턴스에서 아웃바운드 연결을 구성해야 합니다. 자세햔 내용은 [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용 &#40;Transact-SQL &#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)을 참조하세요.  
  
 인바운드 연결 구성은 대개 다음과 같은 단계로 진행됩니다.  
  
1.  다른 시스템에 대한 로그인을 만듭니다.  
  
2.  해당 로그인의 사용자를 만듭니다.  
  
3.  다른 서버 인스턴스의 미러링 엔드포인트에 대한 인증서를 얻습니다.  
  
4.  2단계에서 만든 사용자에 인증서를 연결합니다.  
  
5.  해당 미러링 엔드포인트에 대한 로그인에 CONNECT 권한을 부여합니다.  
  
 미러링 모니터가 있는 경우 그에 대한 인바운드 연결도 설정해야 합니다. 이렇게 하려면 양쪽 파트너 모두에서 미러링 모니터에 대한 로그인, 사용자 및 인증서를 설정해야 합니다.  
  
 다음 절차에서 이러한 단계를 자세히 설명합니다. 각 단계에서는 HOST_A라는 시스템에서 서버 인스턴스를 구성하는 예를 제공합니다. 예 섹션에서는 HOST_B라는 시스템에 또 다른 서버 인스턴스를 구성하는 동일한 단계를 보여 줍니다.  
  
### <a name="to-configure-server-instances-for-inbound-mirroring-connections-on-hosta"></a>인바운드 미러링 연결을 위한 서버 인스턴스를 구성하려면(HOST_A)  
  
1.  다른 시스템에 대한 로그인을 만듭니다.  
  
     다음 예에서는 HOST_A에 있는 서버 인스턴스의 **master** 데이터베이스에서 HOST_B 시스템에 대한 로그인을 만듭니다. 이 예에서 로그인 이름은 `HOST_B_login`입니다. 예제 암호를 자신의 암호로 대체합니다.  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_B_login   
       WITH PASSWORD = '1Sample_Strong_Password!@#';  
    GO  
    ```  
  
     자세한 내용은 [CREATE LOGIN&#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)을 참조하세요.  
  
     이 서버 인스턴스에서 사용자를 보려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
    SELECT * FROM sys.server_principals  
    ```  
  
     자세한 내용은 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)를 참조하세요.  
  
2.  해당 로그인의 사용자를 만듭니다.  
  
     다음 예에서는 이전 단계에서 만든 로그인에 대해 사용자 `HOST_B_user`를 만듭니다.  
  
    ```  
    USE master;  
    CREATE USER HOST_B_user FOR LOGIN HOST_B_login;  
    GO  
    ```  
  
     자세한 내용은 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.  
  
     이 서버 인스턴스에서 로그인을 보려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
    SELECT * FROM sys.sysusers;  
    ```  
  
     자세한 내용은 [sys.sysusers&#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md)를 참조하세요.  
  
3.  다른 서버 인스턴스의 미러링 엔드포인트에 대한 인증서를 얻습니다.  
  
     아웃바운드 연결을 구성할 때 아직 인증서를 가져오지 못했으면 원격 서버 인스턴스의 미러링 엔드포인트에 대한 인증서 사본을 얻습니다. 이렇게 하려면 [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용 &#40;Transact-SQL &#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)에 설명된 대로 해당 서버 인스턴스의 인증서를 백업합니다. 인증서를 다른 시스템으로 복사할 때는 안전한 복사 방법을 사용하세요. 모든 인증서를 안전하게 보관하는 데 많은 주의를 기울여야 합니다.  
  
     자세한 내용은 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)를 참조하세요.  
  
4.  2단계에서 만든 사용자에 인증서를 연결합니다.  
  
     다음 예에서는 HOST_B의 인증서를 HOST_A에 있는 해당 사용자와 연결합니다.  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_B_cert  
       AUTHORIZATION HOST_B_user  
       FROM FILE = 'C:\HOST_B_cert.cer'  
    GO  
    ```  
  
     자세한 내용은 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)를 참조하세요.  
  
     이 서버 인스턴스에서 인증서를 보려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
    SELECT * FROM sys.certificates  
    ```  
  
     자세한 내용은 [sys.certificates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)를 참조하세요.  
  
5.  해당 원격 미러링 엔드포인트에 대한 로그인에 CONNECT 권한을 부여합니다.  
  
     예를 들어 HOST_B에 있는 원격 서버 인스턴스에 대해 HOST_A에서 로컬 로그인에 연결할 권한을 부여하려면 즉, `HOST_B_login`에 연결하려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    USE master;  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_B_login];  
    GO  
    ```  
  
     자세한 내용은 [GRANT 엔드포인트 사용 권한 &#40;Transact-SQL &#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)을 참조하세요.  
  
 이로써 HOST_B에서 HOST_A에 로그인하기 위한 인증서 인증 설정이 끝났습니다.  
  
 이제 HOST_B에서 HOST_A에 대한 같은 인바운드 단계를 수행해야 합니다. 이러한 단계는 아래에 있는 예 섹션의 인바운드 부분 예에 설명되어 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 인바운드 연결을 위한 HOST_B 구성을 보여 줍니다.  
  
> [!NOTE]  
>  이 예제에서는 [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용 &#40;Transact-SQL &#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)의 코드 조각으로 만든 HOST_A 인증서가 포함된 인증서 파일을 사용합니다.  
  
```  
USE master;  
--On HOST_B, create a login for HOST_A.  
CREATE LOGIN HOST_A_login WITH PASSWORD = 'AStrongPassword!@#';  
GO  
--Create a user, HOST_A_user, for that login.  
CREATE USER HOST_A_user FOR LOGIN HOST_A_login  
GO  
--Obtain HOST_A certificate. (See the note   
--   preceding this example.)  
--Asscociate this certificate with the user, HOST_A_user.  
CREATE CERTIFICATE HOST_A_cert  
   AUTHORIZATION HOST_A_user  
   FROM FILE = 'C:\HOST_A_cert.cer';  
GO  
--Grant CONNECT permission for the server instance on HOST_A.  
GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO HOST_A_login  
GO  
```  
  
 자동 장애 조치(failover)를 지원하는 보호 우선 모드에서 실행하려는 경우 아웃바운드 및 인바운드 연결에 대한 미러링 모니터를 구성하기 위해 같은 설정 단계를 반복해야 합니다.  
  
 Transact-SQL 예제를 포함하여 미러 데이터베이스를 만드는 방법은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)를 참조하세요.  
  
 고성능 모드 세션을 설정하는 Transact-SQL 예제는 [예제: 인증서를 사용하여 데이터베이스 미러링 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)를 참조하세요.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 인증서를 다른 시스템으로 복사할 때는 안전한 복사 방법을 사용하세요. 모든 인증서를 안전하게 보관하는 데 많은 주의를 기울여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [GRANT 엔드포인트 사용 권한&amp;#40;Transact-SQL&amp;#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [암호화된 미러 데이터베이스 설정](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [데이터베이스 미러링 엔드포인트&amp;#40;SQL Server&amp;#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [데이터베이스 미러링 구성 문제 해결&#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
