---
title: SQL Server 2017에서 사용되지 않는 데이터베이스 엔진 기능 | Microsoft Docs
titleSuffix: SQL Server 2019
description: 사용되지 않는 데이터베이스 엔진 기능을 알아보세요. 이러한 기능은 SQL Server 2017(14.x)에서도 계속 사용할 수 있지만 새 애플리케이션에서는 사용하면 안 됩니다.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [SQL Server]
- Database Engine [SQL Server], backward compatibility
- deprecation [SQL Server], feature list
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 7ff7a91230daff2aab0e031fa2b87803e379921b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244084"
---
# <a name="deprecated-database-engine-features-in-sql-server-2017"></a>SQL Server 2017에서 사용되지 않는 데이터베이스 엔진 기능

[!INCLUDE[SQL Server 2017](../includes/applies-to-version/sqlserver2017.md)]

  이 항목에서는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 에서 계속 제공되지만 더 이상 사용되지 않는 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]기능에 대해 설명합니다. 새 애플리케이션에는 이러한 기능을 사용하면 안 됩니다.  
  
기능이 사용되지 않는 것으로 표시된 경우 다음을 의미합니다.

- 기능이 유지 관리 모드로만 유지됩니다. 새로운 기능과의 상호 운용성과 관련된 변경 사항을 비롯한 새로운 변경 사항이 적용되지 않습니다.
- 업그레이드를 더욱 용이하게 할 수 있도록 사용되지 않는 기능을 되도록이면 향후 릴리스에서 제거하지 않으려고 합니다. 드문 경우이긴 하지만 이로 인해 향후 혁신에 제한이 있다면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 해당 기능이 영구적으로 제거될 수도 있습니다.
- 새로운 개발 작업에서는 사용되지 않는 기능을 사용하지 않는 것이 좋습니다.      

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Deprecated Features 개체 성능 카운터 및 추적 이벤트를 통해 더 이상 사용되지 않는 기능의 사용을 모니터링할 수 있습니다. 자세한 내용은 [SQL Server 개체 사용](../relational-databases/performance-monitor/use-sql-server-objects.md)을 참조하세요.  

다음 문을 실행하여 이러한 카운터의 값을 사용할 수도 있습니다.  

```sql
SELECT * FROM sys.dm_os_performance_counters
WHERE object_name = 'SQLServer:Deprecated Features';
```

> [!NOTE]
> 이 목록은 [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] 목록과 동일합니다. 사용되지 않거나 지원되지 않는 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] 데이터베이스 엔진 기능에 대해 새로 발표된 것은 없습니다.

## <a name="features-deprecated-in-the-next-version-of-sql-server"></a>다음 버전의 SQL Server에서 사용되지 않는 기능

다음과 같은 SQL Server 데이터베이스 엔진 기능은 다음 버전의 SQL Server에서는 사용되지 않습니다. 새 개발 작업에서는 이러한 기능을 사용하지 말고, 현재 이러한 기능을 사용하는 애플리케이션은 가능한 한 빨리 수정하십시오. **기능 이름** 값은 추적 이벤트에는 ObjectName으로 표시되고 성능 카운터 및 `sys.dm_os_performance_counters`에는 인스턴스 이름으로 표시됩니다. **기능 ID** 값은 추적 이벤트에 ObjectId로 표시됩니다.

### <a name="back-up-and-restore"></a>백업 및 복원

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 | 기능 ID |
|--------------------|-------------|--------------|------------|
| RESTORE { DATABASE &#124; LOG } WITH [MEDIA]PASSWORD는 계속 사용되지 않습니다.<br /><br />BACKUP { DATABASE &#124; LOG } WITH PASSWORD 및 BACKUP { DATABASE &#124; LOG } WITH MEDIAPASSWORD는 더 이상 사용되지 않습니다. | 없음 | BACKUP DATABASE 또는 LOG WITH PASSWORD<br /><br />BACKUP DATABASE 또는 LOG WITH MEDIAPASSWORD | 104<br /><br /> 103 |

### <a name="compatibility-levels"></a>호환성 수준

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 | 기능 ID |
|--------------------|-------------|--------------|------------|
버전 100에서 업그레이드합니다(SQL Server 2008 및 SQL Server 2008 R2). | SQL Server 버전이 더 이상 [지원](https://aka.ms/sqllifecycle)되지 않을 경우 연결된 데이터베이스 호환성 수준이 사용되지 않는 것으로 표시됩니다. 하지만 업그레이드를 더욱 용이하게 하기 위해, 지원되는 데이터베이스 호환성 수준에서 인증된 애플리케이션은 최대한 오래 지원할 예정입니다. 호환성 수준에 대한 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요. | 데이터베이스 호환성 수준 100 | 108 |

### <a name="database-objects"></a>데이터베이스 개체

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 | 기능 ID |
|--------------------|-------------|--------------|------------|
| 트리거에서 결과 집합을 반환하는 기능 | None | 트리거에서 결과 반환 | 12 |

### <a name="encryption"></a>암호화

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 | 기능 ID |
|--------------------|-------------|--------------|------------|
| RC4 또는 RC4_128을 사용한 암호화는 더 이상 사용되지 않으며 다음 버전에서 제거될 예정입니다. RC4 및 RC4_128의 암호 해독은 계속 사용됩니다. | AES 등과 같은 다른 암호화 알고리즘을 사용하십시오. | 사용되지 않는 암호화 알고리즘 | 253 |
| MD2, MD4, MD5, SHA 및 SHA1 사용은 더 이상 사용되지 않습니다. | 대신에 SHA2_256 또는 SHA2_512를 사용합니다. 이전 알고리즘은 계속 작동하지만 사용 중단 이벤트가 발생합니다. |사용되지 않는 해시 알고리즘 | None |

### <a name="remote-servers"></a>원격 서버

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 | 기능 ID |
|--------------------|-------------|--------------|------------|
| sp_addremotelogin<br /><br />sp_addserver <br /><br /> sp_dropremotelogin <br /><br /> sp_helpremotelogin <br /><br /> sp_remoteoption|연결된 서버를 사용하여 원격 서버를 대체합니다. sp_addserver는 로컬 옵션으로만 사용할 수 있습니다. | sp_addremotelogin<br /><br />sp_addserver <br /><br /> sp_dropremotelogin <br /><br /> sp_helpremotelogin <br /><br > sp_remoteoption | 70 <br /><br /> 69 <br /><br /> 71 <br /><br /> 72 <br /><br /> 73 |
| \@\@remserver | 연결된 서버를 사용하여 원격 서버를 대체합니다. | None | None |
| SET REMOTE_PROC_TRANSACTIONS|연결된 서버를 사용하여 원격 서버를 대체합니다. | SET REMOTE_PROC_TRANSACTIONS | 110 |

### <a name="transact-sql"></a>Transact-SQL

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 | 기능 ID |
|--------------------|-------------|--------------|------------|
| **SET ROWCOUNT** , **INSERT**및 **UPDATE**문에 대한 **DELETE** | TOP 키워드 | SET ROWCOUNT | 109 |
| 괄호가 없는 HOLDLOCK 테이블 힌트 | HOLDLOCK에 괄호를 사용합니다. | 괄호가 없는 HOLDLOCK 테이블 힌트 | 167 |

## <a name="features-deprecated-in-a-future-version-of-sql-server"></a>향후 버전의 SQL Server에서 사용되지 않는 기능

다음과 같은 SQL Server 데이터베이스 엔진 기능은 다음 버전의 SQL Server에서 지원됩니다. 어떤 버전의 SQL Server에서 제거될지는 결정되지 않았습니다.

### <a name="back-up-and-restore"></a>백업 및 복원

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| BACKUP { DATABASE &#124; LOG } TO TAPE <br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_tape*|BACKUP { DATABASE &#124; LOG } TO DISK <br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_disk* | BACKUP DATABASE 또는 LOG TO TAPE |
| sp_addumpdevice '**tape**' | sp_addumpdevice '**disk**' | ADDING TAPE DEVICE |
| sp_helpdevice | sys.backup_devices | sp_helpdevice |

### <a name="compatibility-levels"></a>호환성 수준

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sp_dbcmptlevel|ALTER DATABASE ... SET COMPATIBILITY_LEVEL. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요. | sp_dbcmptlevel |
| 데이터베이스 호환성 수준 110 및 120 | 이후 릴리스로 데이터베이스 및 애플리케이션을 업그레이드하도록 계획합니다. 하지만 업그레이드를 더욱 용이하게 하기 위해, 지원되는 데이터베이스 호환성 수준에서 인증된 애플리케이션은 최대한 오래 지원할 예정입니다. 호환성 수준에 대한 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요. | 데이터베이스 호환성 수준 110 <br /><br /> 데이터베이스 호환성 수준 120 |

### <a name="collations"></a>데이터 정렬

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| Korean_Wansung_Unicode <br /><br /> Lithuanian_Classic <br /><br /> SQL_AltDiction_CP1253_CS_AS | 없음 이러한 데이터 정렬은 SQL Server 2005(9.x)에서 지원되기는 하지만 fn_helpcollations를 통해 볼 수는 없습니다. | Korean_Wansung_Unicode <br /><br /> Lithuanian_Classic <br /><br /> SQL_AltDiction_CP1253_CS_AS |
| 힌디어 <br /><br /> 마케도니아어 | 이러한 데이터 정렬은 SQL Server 2005(9.x) 이상에서 지원되기는 하지만 fn_helpcollations를 통해 볼 수는 없습니다. 대신 Macedonian_FYROM_90 및 Indic_General_90을 사용하십시오.|힌디어 <br /><br /> 마케도니아어 |
| Azeri_Latin_90 <br /><br /> Azeri_Cyrilllic_90 | Azeri_Latin_100 <br /><br /> Azeri_Cyrilllic_100 | Azeri_Latin_90 <br /><br /> Azeri_Cyrilllic_90 |

### <a name="data-types"></a>데이터 형식

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sp_addtype <br /><br /> sp_droptype|CREATE TYPE<br /><br /> DROP TYPE | sp_addtype<br /><br /> sp_droptype |
| **timestamp** 데이터 형식에 대한 **rowversion** 구문 | **rowversion** 데이터 형식 구문 | timestamp |
| Null 값을 **timestamp** 열에 삽입하는 기능 | 대신 DEFAULT를 사용합니다. | TIMESTAMP 열에 대한 INSERT NULL |
| 'text in row' 테이블 옵션|**varchar(max)** , **nvarchar(max)** 및 **varbinary(max)** 데이터 형식을 사용합니다. 자세한 내용은 [sp_tableoption&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)을 참조하세요.|Text in row 테이블 옵션 |
| 데이터 형식:<br /><br /> **text**<br /><br /> **ntext**<br /><br /> **image**|**varchar(max)** , **nvarchar(max)** 및 **varbinary(max)** 데이터 형식을 사용합니다.|데이터 형식: **text**, **ntext** 또는 **image** |

### <a name="database-management"></a>데이터베이스 관리

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sp_attach_db <br /><br /> sp_attach_single_file_db|FOR ATTACH 옵션을 사용하는 CREATE DATABASE 문. 하나 이상의 로그 파일에 새 위치가 있는 경우 여러 로그 파일을 다시 작성하려면 FOR ATTACH_REBUILD_LOG 옵션을 사용합니다. | sp_attach_db <br /><br /> sp_attach_single_file_db |
| sp_certify_removable<br /><br /> sp_create_removable|sp_detach_db|sp_certify_removable<br /><br /> sp_create_removable |
| sp_dbremove | DROP DATABASE | sp_dbremove |
| sp_renamedb | ALTER DATABASE의 MODIFY NAME | sp_renamedb |

### <a name="database-objects"></a>데이터베이스 개체

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| CREATE DEFAULT<br /><br /> DROP DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault|CREATE TABLE 및 ALTER TABLE의 DEFAULT 키워드|CREATE_DROP_DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault |
| CREATE RULE<br /><br /> DROP RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule | CREATE TABLE 및 ALTER TABLE의 CHECK 키워드 | CREATE_DROP_RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule |
| sp_change_users_login | ALTER USER를 사용합니다. | sp_change_users_login |
| sp_depends | sys.dm_sql_referencing_entities 및 sys.dm_sql_referenced_entities | sp_depends |
| sp_getbindtoken | MARS 또는 분산 트랜잭션을 사용합니다. | sp_getbindtoken |

### <a name="database-options"></a>데이터베이스 옵션

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sp_bindsession | MARS 또는 분산 트랜잭션을 사용합니다. | sp_bindsession |
| sp_resetstatus | ALTER DATABASE SET { ONLINE &#124; EMERGENCY } | sp_resetstatus
| ALTER DATABASE의 TORN_PAGE_DETECTION 옵션|ALTER DATABASE의 PAGE_VERIFY TORN_PAGE_DETECTION 옵션 | ALTER DATABASE WITH TORN_PAGE_DETECTION |

### <a name="dbcc"></a>DBCC

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| DBCC DBREINDEX|ALTER INDEX의 REBUILD 옵션 | DBCC DBREINDEX |
| DBCC INDEXDEFRAG|ALTER INDEX의 REORGANIZE 옵션 | DBCC INDEXDEFRAG |
| DBCC SHOWCONTIG|sys.dm_db_index_physical_stats | DBCC SHOWCONTIG |
| DBCC PINTABLE<br /><br /> DBCC UNPINTABLE | 아무 효과가 없습니다. | DBCC [UN]PINTABLE |

### <a name="extended-properties"></a>확장 속성

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| 확장 속성을 수준 1 또는 수준 2 유형 개체에 추가하는 Level0type = 'type' 및 Level0type = 'USER' | 확장 속성을 사용자 또는 역할에 직접 추가하는 경우에만 Level0type = 'USER'를 사용합니다.<br /><br /> Level0type = 'SCHEMA'를 사용하여 확장 속성을 TABLE 또는 VIEW와 같은 수준 1 유형이나 COLUMN 또는 TRIGGER와 같은 수준 2 유형에 추가합니다. 자세한 내용은 [sp_addextendedproperty&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)를 참조하세요. | EXTPROP_LEVEL0TYPE<br /><br /> EXTPROP_LEVEL0USER |

### <a name="extended-stored-procedures"></a>확장된 저장 프로시저

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|CREATE LOGIN 사용<br /><br /> SERVERPROPERTY의 DROP LOGIN IsIntegratedSecurityOnly 인수 사용|xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig |

### <a name="extended-stored-procedures-programming"></a>확장 저장 프로시저 프로그래밍

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| srv_alloc<br /><br /> srv_convert<br /><br /> srv_describe<br /><br /> srv_getbindtoken<br /><br /> srv_got_attention<br /><br /> srv_message_handler<br /><br /> srv_paramdata<br /><br /> srv_paraminfo<br /><br /> srv_paramlen<br /><br /> srv_parammaxlen<br /><br /> srv_paramname<br /><br /> srv_paramnumber<br /><br /> srv_paramset<br /><br /> srv_paramsetoutput<br /><br /> srv_paramstatus<br /><br /> srv_paramtype<br /><br /> srv_pfield<br /><br /> srv_pfieldex<br /><br /> srv_rpcdb<br /><br /> srv_rpcname<br /><br /> srv_rpcnumber<br /><br /> srv_rpcoptions<br /><br /> srv_rpcowner<br /><br /> srv_rpcparams<br /><br /> srv_senddone<br /><br /> srv_sendmsg<br /><br /> srv_sendrow<br /><br /> srv_setcoldata<br /><br /> srv_setcollen<br /><br /> srv_setutype<br /><br /> srv_willconvert<br /><br /> srv_wsendmsg | 대신 CLR 통합을 사용하십시오. | XP_API |
| sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc | 대신 CLR 통합을 사용하십시오. | sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc |
| xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|CREATE LOGIN 사용<br /><br /> SERVERPROPERTY의 DROP LOGIN IsIntegratedSecurityOnly 인수 사용 | xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig |

### <a name="high-availability"></a>고가용성

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| 데이터베이스 미러링 | Always On 가용성 그룹<br /><br /> 사용 중인 SQL Server 버전에서 Always On 가용성 그룹을 지원하지 않는 경우에는 로그 전달을 사용하세요. | DATABASE_MIRRORING |

### <a name="index-options"></a>인덱스 옵션

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sp_indexoption | ALTER INDEX | sp_indexoption |
| 옵션 주위에 괄호가 없는 CREATE TABLE, ALTER TABLE 또는 CREATE INDEX 구문 | 현재 구문을 사용하도록 문을 다시 작성해야 합니다. | INDEX_OPTION |

### <a name="instance-options"></a>인스턴스 옵션

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sp_configure의 'allow updates' 옵션|시스템 테이블을 더 이상 업데이트할 수 없습니다. 설정이 아무런 영향을 미치지 않습니다. | sp_configure의 'allow updates' |
| sp_configure 옵션: <br /><br /> 'locks' <br /><br /> 'open objects'<br /><br /> 'set working set size' | 이제 자동으로 구성됩니다. 설정이 아무런 영향을 미치지 않습니다. | sp_configure의 'locks'<br /><br /> sp_configure의 'open objects'<br /><br /> sp_configure의 'set working set size' |
| sp_configure의 'priority boost' 옵션 | 시스템 테이블을 더 이상 업데이트할 수 없습니다. 설정이 아무런 영향을 미치지 않습니다. 대신 Windows start /high ... program.exe 옵션을 사용합니다. | sp_configure의 'priority boost' |
| sp_configure의 'remote proc trans' 옵션 | 시스템 테이블을 더 이상 업데이트할 수 없습니다. 설정이 아무런 영향을 미치지 않습니다. | sp_configure의 'remote proc trans' |

### <a name="linked-servers"></a>연결된 서버

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| 연결된 서버에 대한 SQLOLEDB 공급자를 지정합니다. | SQL Server Native Client(SQLNCLI) | 연결된 서버에 대한 SQLOLEDDB |

### <a name="metadata"></a>메타데이터

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| FILE_ID<br /><br /> INDEXKEY_PROPERTY | FILE_IDEX<br /><br /> sys.index_columns | FILE_ID<br /><br /> INDEXKEY_PROPERTY |

### <a name="native-xml-web-services"></a>네이티브 XML 웹 서비스

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| FOR SOAP 옵션을 사용하는 CREATE ENDPOINT 또는 ALTER ENDPOINT 문<br /><br /> sys.endpoint_webmethods<br /><br /> sys.soap_endpoints|대신 WCF(Windows Communications Foundation) 또는 ASP.NET을 사용해야 합니다. | CREATE/ALTER ENDPOINT<br /><br /> sys.endpoint_webmethods<br /><br /> EXT_soap_endpoints<br /><br /> sys.soap_endpoints |

### <a name="other"></a>기타

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| DB-Library<br /><br />C 언어용 Embedded SQL|데이터베이스 엔진이 DB-Library 및 Embedded SQL API를 사용한 기존 애플리케이션과의 연결을 계속 지원하지만 이들 API를 사용하는 애플리케이션에서 프로그래밍 작업을 수행하는 데 필요한 파일 또는 문서는 포함되지 않습니다. 이후 버전의 SQL Server 데이터베이스 엔진에서는 DB-Library 또는 Embedded SQL 애플리케이션과의 연결이 더 이상 지원되지 않습니다. DB-Library 또는 Embedded SQL을 사용하여 새 애플리케이션을 개발하지 마십시오. 기존의 애플리케이션을 수정할 때 DB-Library 또는 Embedded SQL에 대한 모든 종속 관계를 제거하십시오. 이러한 API 대신 SQLClient 네임스페이스 또는 ODBC 등의 API를 사용하세요. SQL Server 2019(15.x)에는 이러한 애플리케이션을 실행하는 데 필요한 DB-Library DLL이 없습니다. DB-Library 또는 Embedded SQL 애플리케이션을 실행하려면 SQL Server 버전 6.5, SQL Server 7.0 또는 SQL Server 2000(8.x)의 사용 가능한 DB-Library DLL이 있어야 합니다. | None |

### <a name="security"></a>보안

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| ALTER LOGIN WITH SET CREDENTIAL 구문 | 새 ALTER LOGIN ADD 및 DROP CREDENTIAL 구문으로 대체되었습니다. | ALTER LOGIN WITH SET CREDENTIAL |
| sp_addapprole<br /><br /> sp_dropapprole | CREATE APPLICATION ROLE<br /><br /> DROP APPLICATION ROLE | sp_addapprole<br /><br /> sp_dropapprole |
| sp_addlogin<br /><br /> sp_droplogin | CREATE LOGIN<br /><br /> DROP LOGIN|sp_addlogin<br /><br /> sp_droplogin |
| sp_adduser<br /><br /> sp_dropuser | CREATE USER<br /><br /> DROP USER|sp_adduser<br /><br /> sp_dropuser |
| sp_grantdbaccess<br /><br /> sp_revokedbaccess|CREATE USER<br /><br /> DROP USER|sp_grantdbaccess<br /><br /> sp_revokedbaccess |
| sp_addrole<br /><br /> sp_droprole | CREATE ROLE<br /><br /> DROP ROLE|sp_addrole<br /><br /> sp_droprole |
| sp_approlepassword<br /><br /> sp_password | ALTER APPLICATION ROLE<br /><br /> ALTER LOGIN|sp_approlepassword<br /><br /> sp_password |
| sp_changedbowner|ALTER AUTHORIZATION | sp_changedbowner |
| sp_changeobjectowner|ALTER SCHEMA 또는 ALTER AUTHORIZATION | sp_changeobjectowner |
| sp_control_dbmasterkey_password | 마스터 키가 있어야 하며 암호가 정확해야 합니다.|sp_control_dbmasterkey_password |
| sp_defaultdb<br /><br /> sp_defaultlanguage | ALTER LOGIN|sp_defaultdb<br /><br /> sp_defaultlanguage |
| sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin|ALTER LOGIN DISABLE<br /><br /> CREATE LOGIN<br /><br /> DROP LOGIN|sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin |
| USER_ID|DATABASE_PRINCIPAL_ID | USER_ID |
| sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission|이 저장 프로시저가 반환하는 정보는 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]에서는 올바른 것이지만 출력에는 SQL Server 2008에서 구현된 사용 권한 계층에 대한 변경 내용이 반영되지 않습니다. 자세한 내용은 [고정 서버 역할의 권한](https://msdn.microsoft.com/library/ms175892\(SQL.100\).aspx)을 참조하십시오. | sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission |
| GRANT ALL<br /><br /> DENY ALL<br /><br /> REVOKE ALL|GRANT, DENY 및 REVOKE 관련 권한입니다.|ALL 권한 |
| PERMISSIONS 내장 함수 | 대신 sys.fn_my_permissions를 쿼리해야 합니다. | PERMISSIONS |
| SETUSER | EXECUTE AS | SETUSER |
| RC4 및 DESX 암호화 알고리즘|AES 등의 다른 알고리즘을 사용합니다. | DESX 알고리즘 |

### <a name="server-configuration-options"></a>서버 구성 옵션

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| c2 audit 옵션 default trace enabled 옵션<br /><br /> default trace enabled 옵션 | [common criteria compliance enabled 서버 구성 옵션](../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)<br /><br /> [확장 이벤트](../relational-databases/extended-events/extended-events.md) | sp_configure 'c2 audit mode'<br /><br />sp_configure 'default trace enabled' |

### <a name="smo-classes"></a>SMO 클래스

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| *Microsoft.SQLServer. Management.Smo.Information* 클래스<br /><br />*Microsoft.SQLServer. Management.Smo.Settings* 클래스<br /><br />*Microsoft.SQLServer.Management. Smo.DatabaseOptions* 클래스<br /><br />*Microsoft.SqlServer.Management.Smo. DatabaseDdlTrigger.NotForReplication* 속성 | *Microsoft.SqlServer.  Management.Smo.Server* 클래스<br /><br />Microsoft.SqlServer.‘Management.Smo.Server 클래스’<br /><br />Microsoft.SqlServer. Management.Smo.Database* 클래스<br /><br />None | None |

### <a name="sql-server-agent"></a>SQL Server 에이전트

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| **Net Send** 알림<br /><br />호출기 알림 | 이메일 알림<br /><br />이메일 알림 | None |

### <a name="sql-server-management-studio"></a>SQL Server Management Studio

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| SQL Server Management Studio의 솔루션 탐색기 통합 | | None |

### <a name="system-stored-procedures-and-functions"></a>시스템 저장 프로시저와 함수

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sp_db_increased_partitions | 없음 SQL Server 2019(15.x)에서 기본적으로 증가 파티션에 대한 지원을 사용할 수 있습니다. | sp_db_increased_partitions |
| fn_virtualservernodes<br /><br />fn_servershareddrives | sys.dm_os_cluster_nodes<br /><br />sys.dm_io_cluster_shared_drives | fn_virtualservernodes<br /><br /> fn_servershareddrives |
| fn_get_sql | sys.dm_exec_sql_text | fn_get_sql |
| sp_lock | sys.dm_tran_locks | sp_lock |

### <a name="system-tables"></a>시스템 테이블

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sysaltfiles<br /><br />syscacheobjects<br /><br />syscolumns<br /><br />syscomments<br /><br />sysconfigures<br /><br />sysconstraints<br /><br />syscurconfigs<br /><br />sysdatabases<br /><br />sysdepends<br /><br />sysdevices<br /><br />sysfilegroups<br /><br />sysfiles<br /><br />sysforeignkeys<br /><br />sysfulltextcatalogs<br /><br />sysindexes<br /><br />sysindexkeys<br /><br />syslockinfo<br /><br />syslogins<br /><br />sysmembers<br /><br />sysmessages<br /><br />sysobjects<br /><br />sysoledbusers<br /><br />sysopentapes<br /><br />sysperfinfo<br /><br />syspermissions<br /><br />sysprocesses<br /><br />sysprotects<br /><br />sysreferences<br /><br />sysremotelogins<br /><br />sysservers<br /><br />systypes<br /><br />sysusers|호환성 뷰입니다. 자세한 내용은 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)를 참조하세요.<br /><br />**중요:** 호환성 뷰는 SQL Server 2005(9.x)에서 도입된 기능의 메타데이터를 제공하지 않습니다. 애플리케이션에서 카탈로그 뷰를 사용하도록 업그레이드하는 것이 좋습니다. 자세한 내용은 [카탈로그 뷰&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)를 참조하세요. | sysaltfiles<br /><br />syscacheobjects<br /><br />syscolumns<br /><br />syscomments<br /><br />sysconfigures<br /><br />sysconstraints<br /><br />syscurconfigs<br /><br />sysdatabases<br /><br />sysdepends<br /><br />sysdevices<br /><br />sysfilegroups<br /><br />sysfiles<br /><br />sysforeignkeys<br /><br />sysfulltextcatalogs<br /><br />sysindexes<br /><br />sysindexkeys<br /><br />syslockinfo<br /><br />syslogins<br /><br />sysmembers<br /><br />sysmessages<br /><br />sysobjects<br /><br />sysoledbusers<br /><br />sysopentapes<br /><br />sysperfinfo<br /><br />syspermissions<br /><br />sysprocesses<br /><br />sysprotects<br /><br />sysreferences<br /><br />sysremotelogins<br /><br />sysservers<br /><br />systypes<br /><br />sysusers |
| sys.numbered_procedures<br /><br />sys.numbered_procedure_parameters | None | numbered_procedures<br /><br />numbered_procedure_parameters |

### <a name="sql-trace-stored-procedures-functions-and-catalog-views"></a>SQL 추적 저장 프로시저, 함수 및 카탈로그 뷰

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sp_trace_create<br /><br />sp_trace_setevent<br /><br />sp_trace_setfilter<br /><br />sp_trace_setstatus<br /><br />fn_trace_geteventinfo<br /><br />fn_trace_getfilterinfo<br /><br />fn_trace_getinfo<br /><br />fn_trace_gettable<br /><br />sys.traces<br /><br />sys.trace_events<br /><br />sys.trace_event_bindings<br /><br />sys.trace_categories<br /><br />sys.trace_columns<br /><br />sys.trace_subclass_values|[확장 이벤트](../relational-databases/extended-events/extended-events.md) | sp_trace_create<br /><br />sp_trace_setevent<br /><br />sp_trace_setfilter<br /><br />sp_trace_setstatus<br /><br />fn_trace_geteventinfo<br /><br />fn_trace_getfilterinfo<br /><br />fn_trace_getinfo<br /><br />fn_trace_gettable<br /><br />sys.traces<br /><br />sys.trace_events<br /><br />sys.trace_event_bindings<br /><br />sys.trace_categories<br /><br />sys.trace_columns<br /><br />sys.trace_subclass_values |

### <a name="system-views"></a>시스템 뷰

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| sys.sql_dependencies|sys.sql_expression_dependencies|sys.sql_dependencies |

### <a name="table-compression"></a>테이블 압축

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| VarDecimal 스토리지 형식의 사용 | VarDecimal 스토리지 형식은 더 이상 사용되지 않습니다. SQL Server 2019(15.x) 데이터 압축은 10진수 값 이외의 다른 데이터 형식도 압축합니다. VarDecimal 스토리지 형식 대신 데이터 압축을 사용하는 것이 좋습니다. | VarDecimal 스토리지 형식 |
| sp_db_vardecimal_storage_format 프로시저의 사용|VarDecimal 스토리지 형식은 더 이상 사용되지 않습니다. SQL Server 2019(15.x) 데이터 압축은 10진수 값 이외의 다른 데이터 형식도 압축합니다. VarDecimal 스토리지 형식 대신 데이터 압축을 사용하는 것이 좋습니다. | sp_db_vardecimal_storage_format |
| sp_estimated_rowsize_reduction_for_vardecimal 프로시저의 사용|대신 데이터 압축 및 sp_estimate_data_compression_savings 프로시저를 사용합니다. |sp_estimated_rowsize_reduction_for_vardecimal |

### <a name="text-pointers"></a>텍스트 포인터

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| WRITETEXT<br /><br />UPDATETEXT<br /><br />READTEXT|None|UPDATETEXT 또는 WRITETEXT<br /><br />READTEXT |
| TEXTPTR()<br /><br />TEXTVALID() | None | TEXTPTR<br /><br />TEXTVALID |

### <a name="transact-sql"></a>Transact-SQL

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| :: 함수 호출 시퀀스 | SELECT *column_list* FROM sys.\<*function_name*>()으로 바꿉니다.<br /><br />예를 들어 `SELECT * FROM ::fn_virtualfilestats(2,1)`를 `SELECT * FROM sys.fn_virtualfilestats(2,1)`로 대체합니다. | '::' 함수 호출 구문 |
| 세 부분 및 네 부분으로 구성된 열 참조입니다. | 두 부분으로 구성된 이름이 표준 규격 동작입니다.|세 부분 이상으로 구성된 열 이름 |
| SELECT 목록에서 식에 대한 열 별칭으로 사용되는 따옴표로 묶인 문자열<br /><br />'*string_alias*' = *expression* | *expression* [AS] *column_alias*<br /><br />*expression* [AS] [*column_alias*]<br /><br />*expression* [AS] "*column_alias*"<br /><br />*expression* [AS] '*column_alias*'<br /><br />*column_alias* = *expression* | 열 별칭으로 사용되는 문자열 리터럴 |
| 번호를 매긴 프로시저 | 없음 사용하지 마십시오. | ProcNums |
| DROP INDEX의*table_name.index_name* 구문|DROP INDEX의*index_name* ON *table_name* 구문|두 부분으로 구성된 이름을 사용하는 DROP INDEX |
| 세미콜론으로 Transact-SQL 문을 종료하지 않는 경우|세미콜론(;)을 사용하여 Transact-SQL 문을 종료합니다. | None |
| GROUP BY ALL|UNION 또는 파생 테이블과 함께 사용자 지정 사례별 솔루션을 사용합니다. | GROUP BY ALL |
| DML 문의 열 이름으로서 ROWGUIDCOL|$rowguid를 사용합니다.|ROWGUIDCOL |
| DML 문의 열 이름으로서 IDENTITYCOL|$identity를 사용합니다.|IDENTITYCOL |
| 임시 테이블 및 임시 저장 프로시저 이름으로서 # 및 ##의 사용 | 적어도 하나 이상의 추가 문자를 사용해야 합니다.|임시 테이블 및 저장 프로시저의 이름으로 사용되는 '#' 및 '##'
| \@, \@\@ 또는 Transact-SQL 식별자 \@\@의 사용 | \@ 또는 \@\@나 \@\@ 식별자로 시작하는 이름을 사용할 수 없습니다. | ‘\@’ 및 Transact-SQL 식별자 ‘\@\@’으로 시작하는 이름 |
| 기본값으로서 DEFAULT 키워드의 사용|DEFAULT라는 단어를 기본값으로 사용하지 마십시오. | 기본값으로서 DEFAULT 키워드 |
| 테이블 힌트 사이의 구분 기호로서 공백의 사용|쉼표를 사용하여 테이블 힌트를 구분합니다. | 쉼표가 없는 여러 테이블 힌트 |
| 인덱싱된 집계 뷰의 SELECT 목록은 90의 호환성 모드에서 COUNT_BIG(\*)을 포함해야 합니다. | COUNT_BIG(\*)을 사용합니다. | 인덱스 뷰가 COUNT_BIG(\*)이 없는 목록 선택 |
| 뷰를 통해 다중 문 TVF(테이블 반환 함수)를 호출하는 테이블 힌트의 간접 적용|없음|간접 TVF 힌트 |
| ALTER DATABASE 구문:<br /><br />MODIFY FILEGROUP READONLY<br /><br />MODIFY FILEGROUP READWRITE | MODIFY FILEGROUP READ_ONLY<br /><br />MODIFY FILEGROUP READ_WRITE | MODIFY FILEGROUP READONLY<br /><br />MODIFY FILEGROUP READWRITE |
| SET ANSI_NULLS OFF 및 ANSI_NULLS OFF 데이터베이스 옵션<br /><br />SET ANSI_PADDING OFF 및 ANSI_PADDING OFF 데이터베이스 옵션<br /><br />SET CONCAT_NULL_YIELDS_NULL OFF 및 CONCAT_NULL_YIELDS_NULL OFF 데이터베이스 옵션<br /><br />SET OFFSETS | 없음 <br /><br /> ANSI_NULLS, ANSI_PADDING 및 CONCAT_NULLS_YIELDS_NULL은 항상 ON으로 설정됩니다. SET OFFSETS는 사용할 수 없습니다. | SET ANSI_NULLS OFF <br /><br /> SET ANSI_PADDING OFF<br /><br />SET CONCAT_NULL_YIELDS_NULL OFF<br /><br />SET OFFSETS<br /><br />ALTER DATABASE SET ANSI_NULLS OFF<br /><br />ALTER DATABASE SET ANSI_PADDING OFF <br /><br /> ALTER DATABASE SET CONCAT_NULL_YIELDS_NULL OFF |
| SET FMTONLY | [sys.dm_exec_describe_first_result_set&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md), [sys.dm_exec_describe_first_result_set_for_object&#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md), [sp_describe_first_result_set&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 및 [sp_describe_undeclared_parameters&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md). | SET FMTONLY |
| UPDATE 또는 DELETE 문의 FROM 절에 NOLOCK 또는 READUNCOMMITTED 지정 | FROM 절에서 NOLOCK 또는 READUNCOMMITTED 테이블 참고를 제거합니다. | UPDATE 또는 DELETE의 NOLOCK 또는 READUNCOMMITTED |
| WITH 키워드를 사용하지 않고 테이블 힌트 지정 | WITH를 사용합니다. | WITH가 없는 테이블 힌트 |
| INSERT_HINTS | | INSERT_HINTS |

### <a name="tools"></a>도구

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| 추적 캡처용 SQL Server Profiler | SQL Server Management Studio에 포함된 확장 이벤트 프로파일러를 사용합니다.|SQL Server Profiler |
| 추적 재생용 SQL Server Profiler | [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md) |

### <a name="trace-management-objects"></a>Trace Management Objects

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| Microsoft.SqlServer.Management.Trace 네임 스페이스(SQL Server 추적 및 재생 개체용 API 포함)|추적 구성: <xref:Microsoft.SqlServer.Management.XEvent><br /><br />추적 읽기: <xref:Microsoft.SqlServer.XEvent.Linq><br /><br />추적 재생: None | |

### <a name="xml"></a>XML

| 사용되지 않는 기능 | 대체 기능 | 기능 이름 |
|--------------------|-------------|--------------|
| 인라인 XDR 스키마 생성 | XMLDATA 지시어에 FOR XML 옵션은 더 이상 사용되지 않습니다. RAW 및 AUTO 모드의 경우 XSD 생성을 사용하세요. EXPLICT 모드의 XMLDATA 지시어의 경우에는 대체할 옵션이 없습니다. | XMLDATA |

> [!NOTE]
> 현재 **sp_setapprole** 에 대한 쿠키 **OUTPUT** 매개 변수는 정확한 최대 길이인 **varbinary(8000)** 로 정의되어 있습니다. 그러나 현재 구현은 **varbinary(50)** 입니다. 개발자가 **varbinary(50)** 를 할당할 경우 이후 릴리스에서 쿠키 반환 크기가 증가하면 애플리케이션을 변경해야 할 수 있습니다. 이 문제는 사용 중지에 관한 문제는 아니지만 애플리케이션 조정이 유사하기 때문에 이 항목에서 다룹니다. 자세한 내용은 [sp_setapprole&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2016에서 지원되지 않는 데이터베이스 엔진 기능](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)  
  

