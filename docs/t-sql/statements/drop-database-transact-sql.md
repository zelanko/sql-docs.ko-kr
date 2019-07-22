---
title: DROP DATABASE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1fcda20d3efa458808ad9313965feb279a0010c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898101"
---
# <a name="drop-database-transact-sql"></a>DROP DATABASE(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 하나 이상의 사용자 데이터베이스 또는 데이터베이스 스냅샷을 제거합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```
-- SQL Server Syntax
DROP DATABASE [ IF EXISTS ] { database_name | database_snapshot_name } [ ,...n ] [;]
```

```
-- Azure SQL Database, Azure SQL Data Warehouse and Analytics Platform System Syntax
DROP DATABASE database_name [;]
```

## <a name="arguments"></a>인수

*IF EXISTS*
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]~[현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).

이미 있는 경우에만 데이터베이스를 조건부로 삭제합니다.

*database_name* 제거할 데이터베이스의 이름을 지정합니다. 데이터베이스 목록을 표시하려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰를 사용합니다.

*database_snapshot_name*
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]~[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

제거할 데이터베이스 스냅샷의 이름을 지정합니다.

## <a name="general-remarks"></a>일반적인 주의 사항

데이터베이스는 오프라인, 읽기 전용 및 주의 대상과 같은 상태에 관계없이 삭제할 수 있습니다. 데이터베이스의 현재 상태를 표시하려면 **sys.databases** 카탈로그 뷰를 사용합니다.

삭제된 데이터베이스는 백업 복원을 통해서만 다시 만들 수 있습니다. 데이터베이스 스냅샷은 백업할 수 없으므로 복원할 수 없습니다.

데이터베이스가 삭제될 때마다 [master database](../../relational-databases/databases/master-database.md)를 백업해야 합니다.

데이터베이스를 삭제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 데이터베이스가 삭제되며 데이터베이스가 사용하는 물리적 디스크 파일도 삭제됩니다. 삭제 시 데이터베이스 또는 해당 데이터베이스의 파일 중 하나가 오프라인 상태이면 디스크 파일은 삭제되지 않습니다. 이 파일은 Windows 탐색기를 사용해 수동으로 삭제할 수 있습니다. 파일 시스템에서 파일을 삭제하지 않고 현재 서버에서 데이터베이스를 제거하려면 [sp_detach_db](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)를 사용합니다.

> [!WARNING]
> FILE_SNAPSHOT 백업과 연결된 데이터베이스 파일을 제거하는 것은 성공하지만 연결된 스냅샷이 있는 데이터베이스 파일은 해당 데이터베이스 파일을 참조하는 백업이 무효화되는 것을 방지하기 위해 삭제되지 않습니다. 파일은 잘라지지만 FILE_SNAPSHOT 백업을 그대로 유지하기 위해 물리적으로 삭제되지는 않습니다. 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요. **적용 대상**: [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)을 통한 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]입니다.

### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

데이터베이스 스냅샷을 삭제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 데이터베이스 스냅샷이 삭제되고 스냅샷이 사용하는 물리적 NTFS 파일 시스템 스파스 파일도 삭제됩니다. 데이터베이스 스냅샷을 통한 스파스 파일 사용에 대한 자세한 내용은 [데이터베이스 스냅샷](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요. 데이터베이스 스냅샷을 삭제하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 대한 계획 캐시가 삭제됩니다. 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시스토어에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "데이터베이스 유지 관리 또는 재구성 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

## <a name="interoperability"></a>상호 운용성

### <a name="sql-server"></a>SQL Server

트랜잭션 복제를 위해 게시된 데이터베이스 또는 병합 복제를 위해 게시 또는 구독된 데이터베이스를 삭제하려면 먼저 데이터베이스에서 복제를 제거해야 합니다. 데이터베이스가 손상되었거나 복제를 먼저 제거할 수 없거나 또는 두 가지 모두 해당되는 경우, 대부분 ALTER DATABASE를 사용해 데이터베이스를 오프라인으로 설정한 뒤 삭제하는 방식으로 데이터베이스를 삭제할 수 있습니다.

데이터베이스에서 로그 전달 작업을 수행하고 있는 경우 데이터베이스를 삭제하기 전에 로그 전달을 제거하세요. 자세한 내용은 [로그 전달 정보](../../database-engine/log-shipping/about-log-shipping-sql-server.md)를 참조하세요.

## <a name="limitations-and-restrictions"></a>제한 사항

[시스템 데이터베이스](../../relational-databases/databases/system-databases.md)는 삭제할 수 없습니다.

DROP DATABASE 문은 자동 커밋 모드로 실행되어야 하며 명시적이거나 암시적인 트랜잭션에서는 허용되지 않습니다. 자동 커밋 모드는 기본 트랜잭션 관리 모드입니다.

사용 중인 데이터베이스는 삭제할 수 없습니다. 즉, 사용자가 읽기 또는 쓰기 작업을 위해 데이터베이스를 열어 놓은 상태이기 때문입니다. 데이터베이스에서 사용자를 제거하는 한 방법은 ALTER DATABASE를 사용해 데이터베이스를 SINGLE_USER로 설정하는 것입니다.

> [!WARNING]
> 어떤 스레드에 의한 첫 번째 연속 연결이 SINGLE_USER 스레드를 수신하여 연결 실패를 초래하므로 실패로부터 안전한 방식은 아닙니다. SQL Server는 부하 상태에서 데이터베이스를 삭제하는 방법을 기본 제공하지는 않습니다.

### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

데이터베이스를 삭제하려면 먼저 데이터베이스의 모든 데이터베이스 스냅샷을 삭제해야 합니다.

Stretch Database에 대해 활성화된 데이터베이스를 삭제해도 원격 데이터가 제거되지는 않습니다. 원격 데이터를 삭제하려면 수동으로 제거해야 합니다.

### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

데이터베이스를 삭제하려면 master 데이터베이스에 연결해야 합니다.

 DROP DATABASE 문은 SQL 일괄 처리에서 유일한 문이어야 하고 한 번에 하나의 데이터베이스를 삭제할 수 있습니다.

### [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]

데이터베이스를 삭제하려면 master 데이터베이스에 연결해야 합니다.

DROP DATABASE 문은 SQL 일괄 처리에서 유일한 문이어야 하고 한 번에 하나의 데이터베이스를 삭제할 수 있습니다.

## <a name="permissions"></a>사용 권한

### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

데이터베이스에 대한 **CONTROL** 권한, **ALTER ANY DATABASE** 권한 또는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 필요합니다.

### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

프로비전 프로세스를 통해 만들어진 서버 수준의 보안 주체 로그인 또는 **dbmanager** 데이터베이스 역할의 멤버만 데이터베이스를 삭제할 수 있습니다.

### [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

데이터베이스에 대한 **CONTROL** 권한, **ALTER ANY DATABASE** 권한 또는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 필요합니다.

## <a name="examples"></a>예

### <a name="a-dropping-a-single-database"></a>1\. 단일 데이터베이스 삭제

다음 예에서는 `Sales` 데이터베이스를 제거합니다.

```sql
DROP DATABASE Sales;
```

### <a name="b-dropping-multiple-databases"></a>2\. 여러 데이터베이스 삭제

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

다음 예에서는 목록의 데이터베이스 각각을 제거합니다.

```sql
DROP DATABASE Sales, NewSales;
```

### <a name="c-dropping-a-database-snapshot"></a>C. 데이터베이스 스냅샷 삭제

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지

다음 예에서는 원본 데이터베이스에 영향을 주지 않으면서 `sales_snapshot0600`이라는 이름의 데이터베이스 스냅샷을 삭제합니다.

```sql
DROP DATABASE sales_snapshot0600;
```

## <a name="see-also"></a>참고 항목

- [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
