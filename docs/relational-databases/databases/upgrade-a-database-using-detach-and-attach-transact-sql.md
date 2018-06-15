---
title: 분리 및 연결을 사용하여 데이터베이스 업그레이드(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database attaching [SQL Server]
- upgrading databases
- database upgrades [SQL Server]
- database detaching [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 99f66ed9-3a75-4e38-ad7d-6c27cc3529a9
caps.latest.revision: 73
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 28f1aefd634978deeac6d6e9f14a1a102a8e8fbb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32931418"
---
# <a name="upgrade-a-database-using-detach-and-attach-transact-sql"></a>분리 및 연결을 사용하여 데이터베이스 업그레이드(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 분리 및 연결 작업을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 데이터베이스를 업그레이드하는 방법에 대해 설명합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 연결하면 데이터베이스를 바로 사용할 수 있으며 자동으로 업그레이드됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **SQL Server 데이터베이스를 업그레이드하려면**  
  
     [분리 및 연결 작업 사용](#SSMSProcedure)  
  
-   **Follow Up:**  [후속 작업: SQL Server 데이터베이스를 업그레이드한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   시스템 데이터베이스는 연결할 수 없습니다.  
  
-   연결 및 분리는 **데이터베이스 간 소유권 체인** 옵션을 0으로 설정하여 데이터베이스에 대한 데이터베이스 간 소유권 체인을 해제합니다. 체인 설정 방법은 [cross db ownership chaining 서버 구성 옵션](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)을 참조하세요.  
  
-   분리되지 않고 복사된 복제 데이터베이스를 연결하는 경우에는 다음을 수행해야 합니다.  
  
    -   동일한 서버 인스턴스의 업그레이드된 버전에 데이터베이스를 연결하는 경우 연결 작업이 완료된 후 **sp_vupgrade_replication**을 실행하여 복제를 업그레이드해야 합니다. 자세한 내용은 [sp_vupgrade_replication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md)을 참조하세요.  
  
    -   버전에 관계없이 다른 서버 인스턴스에 데이터베이스를 연결하는 경우 연결 작업이 완료된 후 **sp_removedbreplication**을 실행하여 복제를 제거해야 합니다. 자세한 내용은 [sp_removedbreplication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 참조하세요.  
  
###  <a name="Recommendations"></a> 권장 사항  
 알 수 없거나 신뢰할 수 없는 출처의 데이터베이스는 연결 또는 복원하지 않는 것이 좋습니다. 이러한 데이터베이스에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마 또는 물리적 데이터베이스 구조를 수정하여 오류가 발생할 수 있습니다. 알 수 없거나 신뢰할 수 없는 소스의 데이터베이스를 사용하기 전에 비프로덕션 서버의 데이터베이스에서 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 를 실행하여 데이터베이스에서 코드(예: 저장 프로시저 또는 다른 사용자 정의 코드)를 시험해 보세요.  
  
##  <a name="SSMSProcedure"></a> 분리 및 연결을 사용하여 데이터베이스를 업그레이드하려면  
  
1.  데이터베이스를 분리합니다. 자세한 내용은 [데이터베이스 분리](../../relational-databases/databases/detach-a-database.md)를 참조하세요.  
  
2.  필요에 따라 분리된 데이터베이스 파일 및 로그 파일을 이동합니다.  
  
     새 로그 파일을 만들려는 경우에도 데이터 파일뿐만 아니라 로그 파일도 이동해야 합니다. 경우에 따라 데이터베이스를 다시 연결하려면 기존 로그 파일이 필요합니다. 따라서 데이터베이스가 분리된 로그 파일 없이도 성공적으로 연결될 때까지 모든 분리된 로그 파일을 항상 보존하세요.  
  
    > [!NOTE]  
    >  로그 파일을 지정하지 않고 데이터베이스를 연결할 경우 연결 작업은 원래 위치에서 로그 파일을 검색합니다. 로그 파일의 원본이 여전히 원래 위치에 존재하는 경우 해당 복사본이 연결됩니다. 원래 로그 파일을 사용하지 않으려면 새 로그 파일의 경로를 지정하거나 로그 파일의 원본을 새 위치로 복사한 후 제거합니다.  
  
3.  복사한 파일을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스에 연결합니다. 자세한 내용은 [Attach a Database](../../relational-databases/databases/attach-a-database.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 이전 버전의 SQL Server에서 데이터 복사본을 업그레이드합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 연결한 서버 인스턴스에 연결된 쿼리 편집기 창에서 실행됩니다.  
  
1.  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 데이터베이스를 분리합니다.  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'MyDatabase';  
    GO  
    ```  
  
2.  선택한 방법을 사용하여 데이터 및 로그 파일을 새 위치로 복사합니다.  
  
    > [!IMPORTANT]  
    >  프로덕션 데이터베이스의 경우 데이터베이스와 트랜잭션 로그를 별도의 디스크에 저장합니다.  
  
     네트워크를 통해 원격 컴퓨터의 디스크로 파일을 복사하려면 원격 위치의 UNC(Universal Naming Convention) 이름을 사용합니다. UNC 이름은 **\\\\***Servername***\\***Sharename***\\***Path***\\***Filename* 형식입니다. 로컬 하드 디스크에 파일을 쓸 경우 원격 디스크의 파일을 읽거나 파일에 쓰는 데 필요한 해당 권한은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 사용하는 사용자 계정에게 부여되어야 합니다.  
  
3.  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 이동된 데이터베이스와 필요에 따라 해당 로그를 연결합니다.  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyDatabase   
        ON (FILENAME = 'C:\MySQLServer\MyDatabase.mdf'),  
        (FILENAME = 'C:\MySQLServer\Database.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 새로 연결되는 데이터베이스는 개체 탐색기에 즉시 표시되지 않습니다. 데이터베이스를 보려면 개체 탐색기에서 **보기** , **새로 고침**을 차례로 클릭합니다. 개체 탐색기에서 **데이터베이스** 노드가 확장될 때 새로 연결된 데이터베이스가 데이터베이스 목록에 나타납니다.  
  
##  <a name="FollowUp"></a> 후속 작업: SQL Server 데이터베이스를 업그레이드한 후  
 데이터베이스에 전체 텍스트 인덱스가 있는 경우 업그레이드 프로세스는 **upgrade_option** 서버 속성의 설정에 따라 인덱스를 가져오거나, 다시 설정하거나, 다시 작성합니다. 업그레이드 옵션이 가져오기(**upgrade_option** = 2) 또는 다시 작성(**upgrade_option** = 0)으로 설정되어 있는 경우 업그레이드하는 동안 전체 텍스트 인덱스를 사용할 수 없습니다. 인덱싱되는 데이터 양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸릴 수 있습니다. 업그레이드 옵션이 가져오기로 설정되어 있으면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다. **upgrade_option** 서버 속성의 설정을 변경하려면 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)를 사용합니다.  
  
### <a name="database-compatibility-level-after-upgrade"></a>업그레이드 후 데이터베이스 호환성 수준  
 사용자 데이터베이스의 호환성 수준이 업그레이드 이전에 100 이상이면 업그레이드 후에도 동일하게 유지됩니다. 업그레이드 이전에 호환성 수준이 90이면 업그레이드된 데이터베이스에서는 호환성 수준이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되는 가장 낮은 호환성 수준인 100으로 설정됩니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
### <a name="managing-metadata-on-the-upgraded-server-instance"></a>업그레이드한 서버 인스턴스의 메타데이터 관리  
 데이터베이스를 다른 서버 인스턴스에 연결하는 경우 사용자와 응용 프로그램에 일관된 환경을 제공하려면 로그인, 작업, 권한 등 데이터베이스의 일부 또는 모든 메타데이터를 다른 서버 인스턴스에서 다시 만들어야 할 수도 있습니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)을 참조하세요.  
  
### <a name="service-master-key-and-database-master-key-encryption-changes-from-3des-to-aes"></a>3DES에서 AES로의 서비스 마스터 키 및 데이터베이스 마스터 키 암호화 변경  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서는 AES 암호화 알고리즘을 사용하여 SMK(서비스 마스터 키) 및 DMK(데이터베이스 마스터 키)를 보호합니다. AES는 이전 버전에서 사용하는 3DES보다 최신 암호화 알고리즘입니다. 데이터베이스가 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 처음으로 연결되거나 복원될 때 데이터베이스 마스터 키(서비스 마스터 키로 암호화됨)의 복사본은 서버에 아직 저장되지 않은 상태입니다. 데이터베이스 마스터 키를 암호 해독하려면 **OPEN MASTER KEY** 문을 사용해야 합니다. DMK를 암호 해독한 후에는 **ALTER MASTER KEY REGENERATE** 문을 사용하여 SMK(서비스 마스터 키)로 암호화된 DMK의 복사본을 서버에 프로비전함으로써 앞으로 자동 암호 해독을 사용하도록 설정할 수 있습니다. 데이터베이스가 이전 버전에서 업그레이드되지 않은 경우에는 DMK를 다시 생성해야 최신 AES 알고리즘을 사용할 수 있습니다. DMK를 다시 생성하는 방법은 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 데 소요되는 시간은 DMK에서 보호하는 개체 수에 따라 달라집니다. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 작업은 한 번만 필요하며 키 회전 전략의 일부로 이후에 수행하는 다시 생성 작업에 영향을 주지 않습니다.  
  
  
