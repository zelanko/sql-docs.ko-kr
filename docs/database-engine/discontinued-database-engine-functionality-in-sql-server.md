---
title: 중단된 데이터베이스 엔진 기능
description: SQL Server 2019(15.x), SQL Server 2016(13. x) 및 이전 버전에서 중단된 데이터베이스 엔진 기능 및 특성에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 07/22/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- SSL
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= sql-server-linux-2017  || >= sql-server-2016'
ms.openlocfilehash: 73ebe8f968cb3cf91c909ca404c5475f983e2ca6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438820"
---
# <a name="discontinued-database-engine-functionality-in-sql-server"></a>SQL Server에서 중단된 데이터베이스 엔진 기능
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서 더 이상 사용할 수 없는 [!INCLUDE[ssCurrent](../includes/ssnoversion-md.md)]기능에 대해 설명합니다.  

## <a name="discontinued-features-in-sssqlv15"></a>[!INCLUDE[ssSQLv15](../includes/sssqlv15-md.md)]에서 중단된 기능  

- 다음 데이터베이스 범위 구성 옵션은 중단되었습니다.

  - `DISABLE_BATCH_MODE_ADAPTIVE_JOIN`
  - `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK`
  - `DISABLE_INTERLEAVED_EXECUTION_TVF`

현재 구성 옵션은 [ALTER DATABASE SCOPED CONFIGURATION(Transact-SQL)](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조하세요.

>[!NOTE]
>[!INCLUDE[ssSQLv14](../includes/sssqlv14-md.md)]에서 중단된 기능은 없습니다.

## <a name="discontinued-features-in-sssql15"></a>[!INCLUDE[ssSQL15](../includes/sssql15-md.md)]에서 중단된 기능

- [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]는 64비트 애플리케이션입니다. 일부 요소는 32비트 구성 요소로 실행되지만 32비트 설치는 중단되었습니다.  

- 호환성 수준 90이 중단되었습니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  

- ActiveX 하위 시스템이 중단되었습니다. 명령줄 또는 PowerShell 스크립트를 대신 사용 합니다.

- 시작 매개 변수 **-h** 및 **-g**. 자세한 내용은 [Database Engine Service Startup Options](/previous-versions/sql/2014/database-engine/configure-windows/database-engine-service-startup-options?view=sql-server-2014)을(를) 참조하세요.

- SSL(Secure Sockets Layer) 암호화가 더 이상 사용되지 않습니다. 대신 TLS(전송 계층 보안)를 사용해야 합니다. 자세한 내용은 [데이터베이스 엔진에 대해 암호화 연결 사용](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.

## <a name="previous-versions"></a>이전 버전

- [SQL Server 2014에서 지원되지 않는 데이터베이스 엔진 기능](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014)

### <a name="see-also"></a>참고 항목

- [SQL Server 2019에서 사용되지 않는 데이터베이스 엔진 기능](deprecated-database-engine-features-in-sql-server-version-15.md)
- [SQL Server 2017에서 사용되지 않는 데이터베이스 엔진 기능](deprecated-database-engine-features-in-sql-server-2017.md)
- [SQL Server 2016 이후에는 지원되지 않는 데이터베이스 엔진 기능](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)
- [SQL Server 2019 데이터베이스 엔진 기능의 주요 변경 사항](breaking-changes-to-database-engine-features-in-sql-server-version-15.md)
- [SQL Server 2017 데이터베이스 엔진 기능의 주요 변경](breaking-changes-to-database-engine-features-in-sql-server-2017.md)
- [SQL Server 2016 데이터베이스 엔진 기능의 주요 변경](breaking-changes-to-database-engine-features-in-sql-server-2016.md)
- [SQL Server 복제에서 사용되지 않는 기능](../relational-databases/replication/deprecated-features-in-sql-server-replication.md)