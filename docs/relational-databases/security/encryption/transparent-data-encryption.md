---
title: TDE(투명한 데이터 암호화) | Microsoft 문서
description: SQL Server, Azure SQL Database 및 Azure Synapse Analytics 데이터를 암호화하는 투명한 데이터 암호화(미사용 데이터 암호화라고 함)에 대해 알아봅니다.
ms.custom: ''
ms.date: 05/09/2019
ms.prod: sql
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption
- database encryption key, about
- TDE
- database encryption key
- TDE, about
- Transparent Data Encryption, about
- encryption [SQL Server], transparent data encryption
ms.assetid: c75d0d4b-4008-4e71-9a9d-cee2a566bd3b
author: jaszymas
ms.author: jaszymas
ms.reviewer: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d6cd4c4988b07e19c04d72efe2fc19200313f355
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866635"
---
# <a name="transparent-data-encryption-tde"></a>TDE(투명한 데이터 암호화)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

‘TDE’(투명한 데이터 암호화)는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]및 [!INCLUDE[ssSDWfull](../../../includes/sssdwfull-md.md)] 데이터 파일을 암호화합니다. 이 암호화는 미사용 데이터 암호화라고 합니다.

데이터베이스를 보호하기 위해 다음과 같은 예방 조치를 취할 수 있습니다.

* 보안 시스템 디자인
* 기밀 자산 암호화
* 데이터베이스 서버 주변에 방화벽 빌드하기

그러나 드라이브 또는 백업 테이프와 같은 물리적 미디어를 도용하는 악의적인 사용자는 데이터베이스를 복원하거나 연결하여 데이터를 검색할 수 있습니다.

한 가지 해결 방법은 데이터베이스의 중요한 데이터를 암호화하고 인증서를 사용하여 데이터를 암호화하는 데 사용된 키를 보호하는 것입니다. 이 솔루션은 키가 없는 사용자가 데이터를 사용하지 않도록 방지합니다. 그러나 이러한 종류의 보호는 미리 계획해야 합니다.

TDE는 데이터 및 로그 파일에 대한 실시간 I/O 암호화 및 암호 해독을 수행합니다. 암호화는 DEK(데이터베이스 암호화 키)를 사용합니다. 데이터베이스 부팅 레코드는 복구 중에 가용성에 대한 키를 저장합니다. DEK는 대칭 키입니다. 서버의 master 데이터베이스에 저장된 인증서 또는 EKM 모듈이 보호하는 비대칭 키로 보호됩니다.

TDE는 데이터 및 로그 파일인 미사용 데이터를 보호합니다. 이를 통해 다양한 업계에서 확립된 법, 규정 및 지침을 준수할 수 있습니다. 이 기능으로 소프트웨어 개발자는 AES 및 3DES 암호화 알고리즘을 사용하여 기존의 애플리케이션을 변경하지 않고 데이터를 암호화할 수 있습니다.

> [!IMPORTANT]
> TDE에서는 통신 채널을 통한 암호화를 제공하지 않습니다. 통신 채널을 통해 데이터를 암호화하는 방법은 [데이터베이스 엔진에 암호화 연결 사용(SQL Server 구성 관리자)](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.
>
>**관련 항목:**
>
> - [Azure SQL Database를 사용한 투명한 데이터 암호화](/azure/azure-sql/database/transparent-data-encryption-tde-overview)
> - [SQL Data Warehouse에서 TDE(투명한 데이터 암호화) 시작](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql)
> - [다른 SQL Server로 TDE 보호 데이터베이스 이동](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)
> - [EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)
> - [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)
> - [TDE에 대한 SQL Server 보안 블로그(FAQ 포함)](/archive/blogs/sqlsecurity/feature-spotlight-transparent-data-encryption-tde)

## <a name="about-tde"></a>TDE 정보

데이터베이스 파일의 암호화는 페이지 수준에서 수행됩니다. 암호화된 데이터베이스의 페이지는 암호화된 후 디스크에 작성되고 메모리로 읽어 들일 때 암호가 해독됩니다. TDE로 암호화된 데이터베이스의 크기가 증가되지는 않습니다.

### <a name="information-applicable-to-sssds"></a>[!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에 적용되는 정보

[!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] V12에서 TDE를 사용하는 경우, [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에 의해 master 데이터베이스에 저장된 서버 수준 인증서가 자동으로 생성됩니다. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 TDE 데이터베이스를 이동하기 위해 이동 작업에 대한 데이터베이스의 암호를 해독할 필요가 없습니다. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 TDE를 사용하는 방법에 대한 자세한 내용은 [Azure SQL Database를 사용한 투명한 데이터 암호화](/azure/azure-sql/database/transparent-data-encryption-tde-overview)를 참조하세요.

### <a name="information-applicable-to-ssnoversion"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 적용되는 정보

데이터베이스 보안을 설정한 후 올바른 인증서를 사용하여 데이터베이스를 복원할 수 있습니다. 인증서에 대한 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)를 참조하십시오.

TDE를 사용하도록 설정한 후 인증서와 연결된 프라이빗 키를 즉시 백업합니다. 인증서를 사용할 수 없게 되거나 다른 서버에서 데이터베이스를 복원하거나 연결하는 경우 인증서와 프라이빗 키의 백업이 필요합니다. 그렇지 않으면 데이터베이스를 열 수 없습니다.

데이터베이스에서 TDE를 사용하지 않도록 설정한 경우에도 암호화 인증서를 유지합니다. 데이터베이스가 암호화되지 않더라도 트랜잭션 로그의 일부는 보호된 상태로 남아 있을 수 있습니다. 또한 전체 데이터베이스 백업을 수행할 때까지 일부 작업에 대한 인증서가 필요할 수 있습니다.

만료 날짜가 지난 인증서도 여전히 데이터를 TDE로 암호화하고 해독하는 데 사용할 수 있습니다.

### <a name="encryption-hierarchy"></a>암호화 계층

다음 그림에서는 TDE 암호화의 아키텍처를 보여 줍니다. 데이터베이스 수준 항목만(데이터베이스 암호화 키 및 ALTER DATABASE 부분)은 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 TDE를 사용하는 경우 사용자가 구성할 수 있습니다.

![투명한 데이터베이스 암호화 아키텍처](../../../relational-databases/security/encryption/media/tde-architecture.png)

## <a name="enable-tde"></a>TDE 사용

TDE를 사용하려면 다음 단계를 수행합니다.

**적용 대상**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

1. 마스터 키를 만듭니다.

1. 마스터 키로 보호되는 인증서를 만들거나 얻습니다.

1. 데이터베이스 암호화 키를 만들고 인증서를 사용하여 보호합니다.

1. 암호화를 사용하도록 데이터베이스를 설정합니다.

다음 예에서는 `MyServerCert`라는 서버에 설치된 인증서를 사용하여 `AdventureWorks2012` 데이터베이스를 암호화하고 암호를 해독하는 방법을 보여 줍니다.

```sql
USE master;
GO
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';
go
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';
go
USE AdventureWorks2012;
GO
CREATE DATABASE ENCRYPTION KEY
WITH ALGORITHM = AES_128
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;
GO
ALTER DATABASE AdventureWorks2012
SET ENCRYPTION ON;
GO
```

암호화 및 암호 해독 작업은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 의해 백그라운드 스레드로 예약됩니다. 이러한 작업의 상태를 보려면 이 문서의 뒷부분에 나오는 표의 카탈로그 뷰 및 동적 관리 뷰를 사용합니다.

> [!CAUTION]
> TDE가 설정된 데이터베이스의 백업 파일도 데이터베이스 암호화 키를 사용하여 암호화됩니다. 따라서 이러한 백업 파일을 복원하려면 데이터베이스 암호화 키를 보호하는 인증서를 사용할 수 있어야 합니다. 따라서 데이터베이스를 백업하는 것 외에도 서버 인증서의 백업도 유지 관리해야 합니다. 인증서를 더 이상 사용할 수 없을 경우 데이터 손실이 발생합니다.
>
> 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.

## <a name="commands-and-functions"></a>명령 및 함수

다음 문에서 TDE 인증서를 허용하려면 데이터베이스 마스터 키를 사용하여 암호화합니다. 암호만으로 암호화하면 명령문에서는 암호기로서 이것을 거부합니다.

> [!IMPORTANT]
> TDE에서 사용한 후 인증서 암호를 보호하는 경우 다시 시작한 후에는 데이터베이스에 액세스할 수 없게 됩니다.

다음 표에서는 TDE 명령 및 함수에 대한 링크와 설명을 제공합니다.

|명령 또는 함수|목적|
|-------------------------|-------------|
|[CREATE DATABASE ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)|데이터베이스를 암호화하는 키를 만듭니다.| 
|[ALTER DATABASE ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/alter-database-encryption-key-transact-sql.md)|데이터베이스를 암호화하는 키를 변경합니다.|
|[DROP DATABASE ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md)|데이터베이스를 암호화하는 키를 제거합니다.|
|[ALTER DATABASE SET 옵션(TRANSACT-SQL)](../../../t-sql/statements/alter-database-transact-sql-set-options.md)|TDE를 설정하는 데 사용된 **ALTER DATABASE** 옵션에 대해 설명합니다.|

## <a name="catalog-views-and-dynamic-management-views"></a>카탈로그 뷰 및 동적 관리 뷰

 다음 표에서는 TDE 카탈로그 뷰 및 동적 관리 뷰를 보여 줍니다.

|카탈로그 뷰 또는 동적 관리 뷰|목적|
|---------------------------------------------|-------------|
|[sys.databases(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|데이터베이스 정보를 보여 주는 카탈로그 뷰입니다.|
|[sys.certificates(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|데이터베이스의 인증서를 보여 주는 카탈로그 뷰입니다.|
|[sys.dm_database_encryption_keys(Transact-SQL)](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)|데이터베이스 암호화 키 및 암호화의 상태에 대한 정보를 제공하는 동적 관리 뷰입니다.|

## <a name="permissions"></a>사용 권한

위에 표시된 표에서 설명한 것처럼 TDE의 기능 및 명령에는 각각의 사용 권한 요구 사항이 있습니다.

TDE와 관련된 메타데이터를 보려면 인증서에 대한 VIEW DEFINITION 권한이 필요합니다.

## <a name="considerations"></a>고려 사항

처리 중인 데이터베이스 암호화 작업에 대해 재암호화를 검색하는 동안에는 데이터베이스에 대한 유지 관리 작업이 비활성화됩니다. 데이터베이스에 단일 사용자 모드 설정을 사용하여 유지 관리 작업을 수행할 수 있습니다. 자세한 내용은 [단일 사용자 모드로 데이터베이스 설정](../../../relational-databases/databases/set-a-database-to-single-user-mode.md)을 참조하세요.

sys.dm_database_encryption_keys 동적 관리 뷰를 사용하여 데이터베이스 암호화의 상태를 찾을 수 있습니다. 자세한 내용은 이 문서의 앞부분에 나오는 "카탈로그 뷰 및 동적 관리 뷰" 섹션을 참조하세요.

TDE에서는 데이터베이스의 모든 파일 및 파일 그룹이 암호화됩니다. 데이터베이스에 READ ONLY로 표시된 파일 그룹이 있는 경우 데이터베이스 암호화 작업이 실패합니다.

데이터베이스를 데이터베이스 미러링이나 로그 전달에 사용하는 경우 두 데이터베이스 모두 암호화됩니다. 로그 트랜잭션은 암호화되어 전송됩니다.

> [!IMPORTANT]
> 전체 텍스트 인덱스는 데이터베이스에 암호화가 설정될 때 암호화됩니다. SQL Server 2008보다 이전 버전의 SQL Server에서 만든 이러한 인덱스는 SQL Server 2008 이상에서 데이터베이스로 가져오며 TDE로 암호화됩니다.

> [!TIP]
> 데이터베이스의 TDE 상태 변경을 모니터링하려면 SQL Server Audit 또는 SQL Database 감사를 사용합니다. SQL Server의 경우 [SQL Server 감사 동작 그룹 및 동작](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)에서 찾을 수 있는 감사 동작 그룹 DATABASE_CHANGE_GROUP에서 TDE가 추적됩니다.

## <a name="restrictions"></a>제한

초기 데이터베이스 암호화, 키 변경 또는 데이터베이스 암호 해독 중에는 다음 작업이 허용되지 않습니다.

- 데이터베이스의 파일 그룹에서 파일 삭제

- 데이터베이스 삭제

- 데이터베이스를 오프라인 상태로 만들기

- 데이터베이스 분리

- 데이터베이스 또는 파일 그룹을 READ ONLY 상태로 전환

CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY 및 ALTER DATABASE...SET ENCRYPTION 문 실행 중에는 다음 작업이 허용되지 않습니다.

- 데이터베이스의 파일 그룹에서 파일 삭제

- 데이터베이스 삭제

- 데이터베이스를 오프라인 상태로 만들기

- 데이터베이스 분리

- 데이터베이스 또는 파일 그룹을 READ ONLY 상태로 전환

- ALTER DATABASE 명령 사용

- 데이터베이스 또는 데이터베이스 파일 백업 시작

- 데이터베이스 또는 데이터베이스 파일 복원 시작

- 스냅샷 만들기

다음 작업 또는 상태에서는 CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY 및 ALTER DATABASE...SET ENCRYPTION 문을 실행할 수 없습니다.

- 데이터베이스는 읽기 전용이거나 데이터베이스에 읽기 전용 파일 그룹이 포함된 경우

- ALTER DATABASE 명령이 실행 중인 경우

- 데이터 백업이 실행 중인 경우

- 데이터베이스가 오프라인이거나 복원 상태인 경우

- 스냅샷이 진행 중인 경우

- 데이터베이스 유지 관리 태스크가 실행 중인 경우

데이터베이스 파일을 만들 때 TDE가 사용하도록 설정되어 있으면 즉시 파일 초기화를 사용할 수 없습니다.

비대칭 키로 데이터베이스 암호화 키를 암호화하려면 비대칭 키가 확장 가능 키 관리 공급자에 있어야 합니다.

## <a name="tde-scan"></a>TDE 검사

데이터베이스에서 TDE를 사용하도록 설정하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 암호화 검색을 수행해야 합니다. 검색은 데이터 파일에서 버퍼 풀로 각 페이지를 읽은 다음 암호화된 페이지를 디스크에 다시 씁니다.

암호화 검색에 대한 더 많은 제어를 제공하기 위해 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]는 일시 중단 및 다시 시작 구문을 포함하는 TDE 검색을 제공합니다. 시스템의 워크로드가 많거나 업무에 중요한 시간 동안에는 검색을 일시 중지한 후 나중에 검색을 다시 시작할 수 있습니다.

TDE 암호화 검사를 일시 중지하려면 다음 구문을 사용합니다.

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

마찬가지로 TDE 암호화 검사를 다시 시작하려면 다음 구문을 사용합니다.

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

encryption_scan_state 열이 dm_database_encryption_keys 동적 관리 뷰에 추가되었습니다. 암호화 검색의 현재 상태를 표시합니다. 마지막 암호화 검사 상태 변경 날짜와 시간을 포함하는 encryption_scan_modify_date라는 새 열도 있습니다.

암호화 검사가 일시 중단된 상태에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 다시 시작되면 시작 시 오류 로그에 메시지가 기록됩니다. 이 메시지는 기존 검사가 일시 중지되었음을 나타냅니다.

## <a name="tde-and-transaction-logs"></a>TDE 및 트랜잭션 로그

데이터베이스에서 TDE를 사용하여 현재 가상 트랜잭션 로그의 남은 부분을 제거합니다. 제거하면 다음 트랜잭션 로그가 생성됩니다. 이러한 작업은 데이터베이스에 암호화가 설정된 후 로그에 남아 있는 일반 텍스트가 없도록 보장합니다.

로그 파일 암호화의 상태를 찾으려면 이 예에서와 같이 `encryption_state` 뷰의 `sys.dm_database_encryption_keys` 열을 확인합니다.

```sql
USE AdventureWorks2012;
GO
/* The value 3 represents an encrypted state
   on the database and transaction logs. */
SELECT *
FROM sys.dm_database_encryption_keys
WHERE encryption_state = 3;
GO
```

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그 파일 아키텍처에 대한 자세한 내용은 [트랜잭션 로그(SQL Server)](../../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요.

데이터베이스 암호화 키가 변경되기 전에는 이전 데이터베이스 암호화 키가 트랜잭션 로그에 기록된 모든 데이터를 암호화합니다.

데이터베이스 암호화 키를 두 번 변경하는 경우 데이터베이스 암호화 키를 다시 변경하기 전에 먼저 로그 백업을 수행해야 합니다.

## <a name="tde-and-the-tempdb-system-database"></a>TDE 및 tempdb 시스템 데이터베이스

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 다른 데이터베이스가 TDE를 사용하여 암호화된 경우 **tempdb** 시스템 데이터베이스가 암호화됩니다. 이 암호화로 인해 동일한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 암호화되지 않은 데이터베이스의 성능에 영향을 미칠 수 있습니다. **tempdb** 시스템 데이터베이스에 대한 자세한 내용은 [tempdb 데이터베이스](../../../relational-databases/databases/tempdb-database.md)를 참조하세요.

## <a name="tde-and-replication"></a>TDE 및 복제

복제를 수행해도 암호화된 형식의 TDE 설정 데이터베이스에 있는 데이터는 자동으로 복제되지 않습니다. 배포 및 구독자 데이터베이스를 보호하려면 TDE를 개별적으로 설정해야 합니다.

스냅샷 복제는 BCP 파일 같은 암호화되지 않은 중간 파일에 데이터를 저장할 수 있습니다. 트랜잭션 및 병합 복제에 대한 초기 데이터 배포도 가능합니다. 이러한 복제를 수행하는 동안 암호화를 사용하여 통신 채널을 보호할 수 있습니다.

자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용(SQL Server 구성 관리자)](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.

## <a name="tde-and-always-on"></a>TDE 및 Always On    
[Always On 가용성 그룹에 암호화된 데이터베이스를 추가](../../../database-engine/availability-groups/windows/encrypted-databases-with-always-on-availability-groups-sql-server.md)할 수 있습니다.  

가용성 그룹의 일부인 데이터베이스를 암호화하려면 먼저 마스터 키와 인증서를 만들거나 모든 보조 복제본에서 EKM(비대칭 키)을 만든 후에 주 복제본에서 [데이터베이스 암호화 키](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)를 만들어야 합니다.  

DEK(데이터베이스 암호화 키)를 보호하는 데 인증서를 사용하는 경우, 먼저 주 복제본에서 만든 [인증서를 백업](../../../t-sql/statements/backup-certificate-transact-sql.md)한 다음, 모든 보조 복제본에서 [파일에서 인증서를 만든](../../../t-sql/statements/create-certificate-transact-sql.md) 후에 주 복제본에서 데이터베이스 암호화 키를 만들어야 합니다. 

## <a name="tde-and-filestream-data"></a>TDE 및 FILESTREAM 데이터

TDE를 사용하도록 설정한 경우에도 **FILESTREAM** 데이터는 암호화되지 않습니다.

<a name="scan-suspend-resume"></a>

## <a name="remove-tde"></a>TDE 제거

`ALTER DATABASE` 문을 사용하여 데이터베이스에서 암호화를 제거합니다.

```sql
ALTER DATABASE <db_name> SET ENCRYPTION OFF;
```

데이터베이스 상태를 보려면 [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 동적 관리 뷰를 사용합니다.

암호 해독이 완료될 때까지 기다린 후에 [DROP DATABASE ENCRYPTION KEY](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md)를 사용하여 데이터베이스 암호화 키를 제거합니다.

> [!IMPORTANT]
> TDE에 사용되는 마스터 키와 인증서를 안전한 위치에 백업합니다. 마스터 키와 인증서는 데이터베이스가 TDE로 암호화될 때 만들어진 백업을 복원하는 데 필요합니다. 데이터베이스 암호화 키를 제거한 후에는 로그 백업을 수행한 다음, 암호 해독된 데이터베이스의 새로운 전체 백업을 수행합니다. 

## <a name="tde-and-buffer-pool-extension"></a>TDE 및 버퍼 풀 확장

TDE를 사용하여 데이터베이스를 암호화한 경우에 BPE(버퍼 풀 확장)와 관련된 파일은 암호화되지 않습니다. 해당 파일에는 파일 시스템 수준에서 BitLocker 또는 EFS와 같은 암호화 도구를 사용합니다.

## <a name="tde-and-in-memory-oltp"></a>TDE 및 메모리 내 OLTP

TDE는 메모리 내 OLTP 개체가 포함된 데이터베이스에서 TDE를 사용할 수 있습니다. TDE를 사용하는 경우 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 및 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 메모리 내 OLTP 로그 레코드와 데이터가 암호화됩니다. TDE를 사용하지만 MEMORY_OPTIMIZED_DATA 파일 그룹의 파일이 암호화되지 않으면 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 메모리 내 OLTP 로그 레코드와 데이터가 암호화됩니다.

## <a name="related-tasks"></a>관련 작업

[다른 SQL Server로 TDE 보호 데이터베이스 이동](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
[EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
[Azure Key Vault(SQL Server)를 사용한 확장 가능 키 관리](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  

## <a name="related-content"></a>관련 콘텐츠

[Azure SQL Database를 사용한 투명한 데이터 암호화](/azure/azure-sql/database/transparent-data-encryption-tde-overview)  
[SQL Data Warehouse에서 TDE(투명한 데이터 암호화) 시작](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql)  
[SQL Server 암호화](../../../relational-databases/security/encryption/sql-server-encryption.md)  
[SQL Server 및 데이터베이스 암호화 키(데이터베이스 엔진)](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

## <a name="see-also"></a>참고 항목

[SQL Server 데이터베이스 엔진 및 Azure SQL Database 보안 센터](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[FILESTREAM [SQL Server]](../../../relational-databases/blob/filestream-sql-server.md)