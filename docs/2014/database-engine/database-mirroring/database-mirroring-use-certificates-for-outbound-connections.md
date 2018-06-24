---
title: 데이터베이스 미러링 끝점의 아웃 바운드 연결 (Transact SQL)에 대 한 인증서 사용 허용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- certificates [SQL Server], database mirroring
- outbound connections [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 464c9096-10d6-4c5e-8bb1-19acba27ad9e
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e24b2736e4643627aa16040f2eca5d7515067730
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081634"
---
# <a name="allow-a-database-mirroring-endpoint-to-use-certificates-for-outbound-connections-transact-sql"></a>데이터베이스 미러링 끝점의 아웃바운드 연결에 대한 인증서 사용 허용(Transact-SQL)
  이 항목에서는 인증서를 사용하여 데이터베이스 미러링의 아웃바운드 연결을 인증하도록 서버 인스턴스를 구성하는 단계를 설명합니다. 아웃바운드 연결을 구성한 후 인바운드 연결을 설정할 수 있습니다.  
  
> [!NOTE]  
>  서버 인스턴스의 모든 미러링 연결은 단일 데이터베이스 미러링 끝점을 사용하며 이러한 끝점을 만들 때는 서버 인스턴스의 인증 방법을 지정해야 합니다.  
  
 아웃바운드 연결 구성은 대개 다음과 같은 단계로 진행됩니다.  
  
1.  **master** 데이터베이스에서 데이터베이스 마스터 키를 만듭니다.  
  
2.  **master** 데이터베이스에서 서버 인스턴스의 암호화된 인증서를 만듭니다.  
  
3.  서버 인스턴스의 인증서를 사용하여 해당 인스턴스의 끝점을 만듭니다.  
  
4.  인증서를 파일에 백업한 다음 안전한 다른 시스템으로 복사합니다.  
  
 파트너와 미러링 모니터 각각에 대해 이러한 단계를 완료해야 합니다.  
  
 다음 절차에서 이러한 단계를 자세히 설명합니다. 각 단계에서는 HOST_A라는 시스템에서 서버 인스턴스를 구성하는 예를 제공합니다. 예 섹션에서는 HOST_B라는 시스템에 또 다른 서버 인스턴스를 구성하는 동일한 단계를 보여 줍니다.  
  
## <a name="procedure"></a>프로시저  
  
#### <a name="to-configure-server-instances-for-outbound-mirroring-connections-on-hosta"></a>아웃바운드 미러링 연결을 위한 서버 인스턴스를 구성하려면(HOST_A)  
  
1.  **master** 데이터베이스에 데이터베이스 마스터 키가 없으면 새로 만듭니다. 데이터베이스의 기존 키를 보려면 [sys.symmetric_keys](/sql/relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql) 카탈로그 뷰를 사용합니다.  
  
     데이터베이스 마스터 키를 만들려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 사용합니다.  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<1_Strong_Password!>';  
    GO  
    ```  
  
     고유하고 강력한 암호를 사용하고 암호를 기록하여 안전한 곳에 보관합니다.  
  
     자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql) 및 [데이터베이스 마스터 키 만들기](../../relational-databases/security/encryption/create-a-database-master-key.md)를 참조하세요.  
  
2.  **master** 데이터베이스에서 데이터베이스 미러링을 위한 아웃바운드 연결에 사용할 암호화된 인증서를 서버 인스턴스에 만듭니다.  
  
     예를 들어 HOST_A 시스템의 인증서를 만들려면 다음 코드를 사용합니다.  
  
    > [!IMPORTANT]  
    >  인증서를 1년 이상 사용하려는 경우 CREATE CERTIFICATE 문에 EXPIRY_DATE 옵션을 사용하여 UTC 시간으로 만료 날짜를 지정합니다. 또한 SQL Server Management Studio를 사용하여 인증서 만료 시 경고를 표시하는 정책 기반 관리 규칙을 만드는 것이 좋습니다. 정책 관리의 **새 조건 만들기** 대화 상자를 사용하여 **@ExpirationDate** 패싯의 **@ExpirationDate** 필드에 이 규칙을 만듭니다. 자세한 내용은 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md) 및 [SQL Server 보안 설정](../../relational-databases/security/securing-sql-server.md)을 참조하세요.  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_A_cert   
       WITH SUBJECT = 'HOST_A certificate for database mirroring',   
       EXPIRY_DATE = '11/30/2013';  
    GO  
    ```  
  
     자세한 내용은 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)를 참조하세요.  
  
     **master** 데이터베이스에 있는 인증서를 보려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    USE master;  
    SELECT * FROM sys.certificates;  
    ```  
  
     자세한 내용은 [sys.certificates&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-certificates-transact-sql)를 참조하세요.  
  
3.  서버 인스턴스마다 데이터베이스 미러링 끝점이 있는지 확인합니다.  
  
     서버 인스턴스의 데이터베이스 미러링 끝점이 이미 있으면 서버 인스턴스에서 설정하는 다른 모든 세션에 해당 끝점을 다시 사용해야 합니다. 서버 인스턴스에 데이터베이스 미러링 끝점이 있는지 확인하고 해당 구성을 보려면 다음 문을 사용합니다.  
  
    ```  
    SELECT name, role_desc, state_desc, connection_auth_desc, encryption_algorithm_desc   
       FROM sys.database_mirroring_endpoints;  
    ```  
  
     끝점이 없으면 아웃바운드 연결에는 이 인증서를 사용하고 다른 시스템의 확인에는 이 인증서의 자격 증명을 사용하는 끝점을 만듭니다. 이 끝점은 서버 인스턴스가 참여하는 모든 미러링 세션에 사용되는 서버 차원의 끝점입니다.  
  
     예를 들어 HOST_A에 예제 서버 인스턴스의 미러링 끝점을 만들려면 다음 코드를 사용합니다.  
  
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
  
     자세한 내용은 [CREATE ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)를 참조하세요.  
  
4.  인증서를 백업하고 다른 시스템에 복사합니다. 다른 시스템에서 인바운드 연결을 구성하는 데 이 인증서가 필요합니다.  
  
    ```  
    BACKUP CERTIFICATE HOST_A_cert TO FILE = 'C:\HOST_A_cert.cer';  
    GO  
    ```  
  
     자세한 내용은 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)를 참조하세요.  
  
     안전한 방법으로 이 인증서를 복사합니다. 모든 인증서를 안전하게 보관하는 데 많은 주의를 기울여야 합니다.  
  
 앞 단계의 예제 코드에서는 HOST_A에 아웃바운드 연결을 구성합니다.  
  
 이제 HOST_B에 대해 동일한 아웃바운드 단계를 수행해야 합니다. 이러한 단계는 다음 예 섹션에 설명되어 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 아웃바운드 연결을 위한 HOST_B 구성을 보여 줍니다.  
  
```  
USE master;  
--Create the database Master Key, if needed.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Strong_Password_#2>';  
GO  
-- Make a certifcate on HOST_B server instance.  
CREATE CERTIFICATE HOST_B_cert   
   WITH SUBJECT = 'HOST_B certificate for database mirroring',   
   EXPIRY_DATE = '11/30/2013';  
GO  
--Create a mirroring endpoint for the server instance on HOST_B.  
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
--Backup HOST_B certificate.  
BACKUP CERTIFICATE HOST_B_cert TO FILE = 'C:\HOST_B_cert.cer';  
GO   
--Using any secure copy method, copy C:\HOST_B_cert.cer to HOST_A.  
```  
  
 원하는 안전한 방법으로 인증서를 다른 시스템에 복사합니다. 모든 인증서를 안전하게 보관하는 데 많은 주의를 기울여야 합니다.  
  
> [!IMPORTANT]  
>  아웃바운드 연결을 설정한 후에는 다른 서버 인스턴스에 대해 각 서버 인스턴스에서 인바운드 연결을 구성해야 합니다. 자세햔 내용은 [데이터베이스 미러링 끝점의 인바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)을 참조하세요.  
  
 Transact-SQL 예제를 포함하여 미러 데이터베이스를 만드는 방법은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)를 참조하세요.  
  
 고성능 모드 세션을 설정하는 Transact-SQL 예제는 [예제: 인증서를 사용하여 데이터베이스 미러링 설정&#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)를 참조하세요.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 네트워크 보안을 보장할 수 없는 경우 데이터베이스 미러링 연결에 암호화를 사용하는 것이 좋습니다.  
  
 인증서를 다른 시스템으로 복사할 때는 안전한 복사 방법을 사용하세요.  
  
## <a name="see-also"></a>관련 항목  
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [ALTER ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)   
 [예제: 인증서를 사용하여 데이터베이스 미러링 설정&#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)   
 [데이터베이스 미러링 끝점&#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [데이터베이스 미러링 구성 문제 해결&#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [암호화된 미러 데이터베이스 설정](set-up-an-encrypted-mirror-database.md)  
  
  
