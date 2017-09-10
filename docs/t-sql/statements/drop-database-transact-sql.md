---
title: DROP DATABASE (TRANSACT-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE
- DROP_DATABASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], deleting
- removing databases
- database snapshots [SQL Server], removing
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- DROP DATABASE statement
- database removal [SQL Server], DROP DATABASE statement
ms.assetid: 477396a9-92dc-43c9-9b97-42c8728ede8e
caps.latest.revision: 83
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 347995e21c5930007404fd8a9dd8bb29d9879981
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-database-transact-sql"></a>DROP DATABASE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 하나 이상의 사용자 데이터베이스 또는 데이터베이스 스냅숏을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- SQL Server Syntax  
DROP DATABASE [ IF EXISTS ] { database_name | database_snapshot_name } [ ,...n ] [;]  
```  
  
```  
-- Azure SQL Database and Parallel Data Warehouse Syntax   
DROP DATABASE database_name [;]  
```  
  
## <a name="arguments"></a>인수  
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 조건에 따라 이미 있는 경우에 데이터베이스를 삭제 합니다.  
  
 *database_name*  
 제거할 데이터베이스의 이름을 지정합니다. 사용 하 여 데이터베이스의 목록을 표시 하려면는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 *database_snapshot_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 제거할 데이터베이스 스냅숏의 이름을 지정합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 데이터베이스는 오프라인, 읽기 전용 및 주의 대상과 같은 상태에 관계없이 삭제할 수 있습니다. 데이터베이스의 현재 상태를 표시 하려면 사용 된 **sys.databases** 카탈로그 뷰.  
  
 삭제된 데이터베이스는 백업 복원을 통해서만 다시 만들 수 있습니다. 데이터베이스 스냅숏은 백업할 수 없으므로 복원할 수 없습니다.  
  
 데이터베이스를 삭제할 때는 [master 데이터베이스](../../relational-databases/databases/master-database.md) 를 백업 해야 합니다.  
  
 데이터베이스를 삭제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 데이터베이스가 삭제되며 데이터베이스가 사용하는 물리적 디스크 파일도 삭제됩니다. 삭제 시 데이터베이스 또는 해당 데이터베이스의 파일 중 하나가 오프라인 상태이면 디스크 파일은 삭제되지 않습니다. 이 파일은 Windows 탐색기를 사용해 수동으로 삭제할 수 있습니다. 파일 시스템에서 파일을 삭제 하지 않고 현재 서버에서 데이터베이스 제거를 사용 하 여 [sp_detach_db](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)합니다.  
  
> [!WARNING]  
>  FILE_SNAPSHOT 있는 데이터베이스를 삭제 하는 중 연결 된 백업이 성공 하지만 연결 된 스냅숏이 있는 데이터베이스 파일 백업을이 데이터베이스 파일에 참조를 무효화를 방지 하기 삭제 되지 않습니다. 파일을 자를 수 있지만 FILE_SNAPSHOT 백업의 그대로 유지 하기 위해 물리적으로 삭제 되지 않습니다. 자세한 내용은 [Microsoft Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요. **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)합니다.  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 데이터베이스 스냅숏을 삭제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 데이터베이스 스냅숏이 삭제되고 스냅숏이 사용하는 물리적 NTFS 파일 시스템 스파스 파일도 삭제됩니다. 데이터베이스 스냅숏의 스파스 파일을 사용 하는 방법에 대 한 정보를 참조 하십시오. [데이터베이스 스냅숏 &#40; SQL Server &#41; ](../../relational-databases/databases/database-snapshots-sql-server.md). 데이터베이스 스냅숏을 삭제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 대한 계획 캐시가 삭제됩니다. 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.  
  
## <a name="interoperability"></a>상호 운용성  
  
### <a name="sql-server"></a>SQL Server  
 트랜잭션 복제를 위해 게시된 데이터베이스 또는 병합 복제를 위해 게시 또는 구독된 데이터베이스를 삭제하려면 먼저 데이터베이스에서 복제를 제거해야 합니다. 데이터베이스가 손상되었거나 복제를 먼저 제거할 수 없거나 또는 두 가지 모두 해당되는 경우, 대부분 ALTER DATABASE를 사용해 데이터베이스를 오프라인으로 설정한 뒤 삭제하는 방식으로 데이터베이스를 삭제할 수 있습니다.  
  
 데이터베이스에서 로그 전달 작업을 수행하고 있는 경우 데이터베이스를 삭제하기 전에 로그 전달을 제거하세요. 자세한 내용은 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)를 참조하세요.  
  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 [시스템 데이터베이스](../../relational-databases/databases/system-databases.md) 삭제할 수 없습니다.  
  
 DROP DATABASE 문은 자동 커밋 모드로 실행되어야 하며 명시적이거나 암시적인 트랜잭션에서는 허용되지 않습니다. 자동 커밋 모드는 기본 트랜잭션 관리 모드입니다.  
  
 사용 중인 데이터베이스는 삭제할 수 없습니다. 즉, 사용자가 읽기 또는 쓰기 작업을 위해 데이터베이스를 열어 놓은 상태이기 때문입니다. 데이터베이스에서 사용자를 제거하려면 ALTER DATABASE를 사용해 데이터베이스를 SINGLE_USER로 설정하세요.  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 데이터베이스를 삭제하려면 먼저 데이터베이스의 모든 데이터베이스 스냅숏을 삭제해야 합니다.  
  
 스트레치 데이터베이스에 대 한 데이터베이스 사용을 삭제 하는 중입니다. 원격 데이터는 제거 되지 않습니다. 원격 데이터를 삭제 하려는 경우 수동으로 제거 해야 합니다.  
  
### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 데이터베이스를 삭제하려면 master 데이터베이스에 연결해야 합니다.  
  
 DROP DATABASE 문은 SQL 일괄 처리에서 유일한 문이어야 하고 한 번에 하나의 데이터베이스를 삭제할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 필요는 **제어** 데이터베이스에 대 한 권한 또는 **ALTER ANY DATABASE** 권한 또는 멤버 자격에는 **db_owner** 고정된 데이터베이스 역할입니다.  
  
### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 (프로 비전 프로세스로 만들어진) 서버 수준 보안 주체 로그인 또는의 멤버는 **dbmanager** 데이터베이스 역할에서 데이터베이스를 삭제할 수 있습니다.  
  
### [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 필요는 **제어** 데이터베이스에 대 한 권한 또는 **ALTER ANY DATABASE** 권한 또는 멤버 자격에는 **db_owner** 고정된 데이터베이스 역할입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-single-database"></a>1. 단일 데이터베이스 삭제  
 다음 예에서는 `Sales` 데이터베이스를 제거합니다.  
  
```  
DROP DATABASE Sales;  
```  
  
### <a name="b-dropping-multiple-databases"></a>2. 여러 데이터베이스 삭제  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 다음 예에서는 각 나열된 된 데이터베이스를 제거 합니다.  
  
```  
DROP DATABASE Sales, NewSales;  
```  
  
### <a name="c-dropping-a-database-snapshot"></a>3. 데이터베이스 스냅숏 삭제  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 다음 예에서는 원본 데이터베이스에 영향을 주지 않으면서 `sales`_`snapshot0600`이라는 이름의 데이터베이스 스냅숏을 삭제합니다.  
  
```  
DROP DATABASE sales_snapshot0600;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  

