---
title: 스트레치 사용 데이터베이스 복원(Stretch Database) | Microsoft 문서
ms.date: 07/06/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cebc1f6d-d5ea-460d-ae60-d047d29c2723
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 479d632b8d5413de9517f92f604c44383012acab
ms.sourcegitcommit: ec1f01b4bb54621de62ee488decf9511d651d700
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56240797"
---
# <a name="restore-stretch-enabled-databases-stretch-database"></a>스트레치 사용 데이터베이스 복원(Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  필요한 경우 백업된 데이터베이스를 복원하면 다양한 유형의 실패, 오류 및 재해로부터 복구하는 데 도움이 됩니다.
  
  백업에 대한 자세한 내용은 [스트레치 사용 데이터베이스 백업](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)을 참조하세요.

> [!TIP]
> 백업은 전체 고가용성 및 무중단 업무 방식 솔루션의 한 부분일 뿐입니다. 고가용성에 대한 자세한 내용은 [고가용성 솔루션](../../database-engine/sql-server-business-continuity-dr.md)을 참조하세요.

## <a name="restore-your-sql-server-data"></a>SQL Server 데이터 복원
하드웨어 오류 또는 손상을 복구하려면 백업에서 스트레치 사용 SQL Server 데이터베이스를 복원합니다. 현재 사용하는 SQL Server 복원 방법을 계속 사용할 수 있습니다. 자세한 내용은 [복원 및 복구 개요](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)를 참조하세요.

SQL Server 데이터베이스를 복원한 후 저장 프로시저 **sys.sp_rda_reauthorize_db** 를 실행하여 스트레치 사용 SQL Server 데이터베이스와 원격 Azure 데이터베이스 간을 다시 연결해야 합니다. 자세한 내용은 [SQL Server 데이터베이스와 원격 Azure 데이터베이스 간 연결 복원](#reconnect)을 참조하세요.

## <a name="restore-your-remote-azure-data"></a>원격 Azure 데이터 복원

### <a name="recover-a-live-azure-database"></a>라이브 Azure 데이터베이스 복구
Azure의 SQL Server 스트레치 데이터베이스 서비스는 Azure Storage 스냅숏을 사용하여 적어도 8시간마다 모든 라이브 데이터의 스냅숏을 만듭니다. 이러한 스냅숏은 7일 동안 유지됩니다. 따라서 마지막 스냅숏이 만들어진 시간까지 지난 7일 내에 적어도 21개 지점 중 하나로 데이터를 복원할 수 있습니다.

Azure 포털을 사용하여 라이브 Azure 데이터베이스를 이전 시점으로 복원하려면 다음을 수행합니다.

1. [Azure 포털][]에 로그인합니다.
2. 화면 왼쪽에서 **찾아보기** 를 선택한 다음 **SQL 데이터베이스**를 선택합니다.
3. 데이터베이스를 찾아서 선택합니다.
4. 데이터베이스 블레이드 맨 위에서 **복원**을 클릭합니다.
5. 새 **데이터베이스 이름**을 지정하고 **복원 지점** 을 선택한 다음 **만들기**를 클릭합니다.
6. 데이터베이스 복원 프로세스가 시작되고 **알림**을 사용하여 모니터링할 수 있습니다.

### <a name="recover-a-deleted-azure-database"></a>삭제된 Azure 데이터베이스 복구
Azure의 SQL Server 스트레치 데이터베이스 서비스는 데이터베이스가 삭제되기 전에 데이터베이스 스냅숏을 만들어 7일간 보유합니다. 이후에는 라이브 데이터베이스에서 더 이상 스냅숏을 보유하지 않습니다. 이렇게 하면 삭제된 데이터베이스를 삭제된 시점으로 복원할 수 있습니다.

Azure 포털을 사용하여 삭제된 Azure 데이터베이스를 삭제된 시점으로 복원하려면 다음을 수행합니다.

1. [Azure 포털][]에 로그인합니다.
2. 화면 왼쪽에서 **찾아보기** 를 선택한 다음 **SQL Server**를 선택합니다.
3. 서버를 찾아서 선택합니다.
4. 서버 블레이드의 작업까지 아래로 스크롤하여 **삭제된 데이터베이스** 타일을 클릭합니다.
5. 복원하려는 삭제된 데이터베이스를 선택합니다.
5. 새 **데이터베이스 이름** 을 지정하고 **만들기**를 클릭합니다.
6. 데이터베이스 복원 프로세스가 시작되고 **알림**을 사용하여 모니터링할 수 있습니다.

## <a name="reconnect"></a>SQL Server 데이터베이스와 원격 Azure 데이터베이스 간 연결 복원

1.  다른 이름으로 또는 다른 영역에 복원된 Azure 데이터베이스에 연결하려는 경우 저장 프로시저 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) 를 실행하여 이전 Azure 데이터베이스와의 연결을 끊습니다.  
  
2.  저장 프로시저 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 를 실행하여 Azure 데이터베이스에 로컬 스트레치 사용 데이터베이스를 다시 연결합니다.  
  
    -   sysname 또는 varchar(128) 값으로 기존 데이터베이스 범위 자격 증명을 제공합니다. (Varchar(max)를 사용하지 마십시오.) **sys.database_scoped_credentials** 뷰에서 자격 증명 이름을 조회할 수 있습니다.  
  
    -   원격 데이터의 복사본을 만들고 복사본에 연결할 것인지 지정합니다(권장).  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    EXEC sp_rda_reauthorize_db
        @credential = N'<existing_database_scoped_credential_name>',
        @with_copy = 1 ;  
    GO  
    ```  
    
  ## <a name="see-also"></a>참고 항목  
 [스트레치 사용 데이터베이스 백업](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
 [스트레치 데이터베이스 관리 및 문제 해결](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 
 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)  
 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
 
 [Azure 포털]: https://portal.azure.com/
 
