---
title: SQL Server, Deprecated Features 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Deprecated Features
- performance counters [SQL Server], deprecated features
- deprecation [SQL Server], performance counters
- Deprecated Features object
ms.assetid: e95de9d6-c950-41cd-8aaa-be529c6de198
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6437ede86133d12622376700cfac5070dabd8fd6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68206957"
---
# <a name="sql-server-deprecated-features-object"></a>SQL Server, Deprecated Features 개체
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 SQLServer:Deprecated Features 개체는 사용되지 않는 기능으로 지정된 기능을 모니터링하는 카운터를 제공합니다. 이 카운터는 경우에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 마지막으로 시작된 이후로 사용되지 않는 기능이 발견된 횟수를 나열하는 사용 카운트를 제공합니다.  
  
 다음 표에서는 SQL Server Deprecated Features 카운터 인스턴스에 대해 설명합니다.  
  
|SQL Server Deprecated Features 카운터 인스턴스|설명|  
|------------------------------------------------------|-----------------|  
|임시 테이블 및 저장 프로시저의 이름으로 사용되는 '#' 및 '##'|# 외에 다른 문자를 포함하지 않는 식별자가 발견되었습니다. 적어도 하나 이상의 추가 문자를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|'::' 함수 호출 구문|테이블 반환 함수에 대해 :: 함수 호출 구문이 발견되었습니다. `SELECT column_list FROM` * \< Function_name>* `()`으로 대체 합니다. 예를 들어 `SELECT * FROM ::fn_virtualfilestats(2,1)`를 `SELECT * FROM sys.fn_virtualfilestats(2,1)`로 대체합니다. 컴파일마다 한 번씩 발생합니다.|  
|‘\@’ 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자 ‘\@\@’으로 시작하는 이름|\@ 또는 \@\@으로 시작하는 식별자가 발견되었습니다. \@ 또는 \@\@나 \@\@ 식별자로 시작하는 이름을 사용할 수 없습니다. 컴파일마다 한 번씩 발생합니다.|  
|ADDING TAPE DEVICE|사용 되지 않는 기능 sp_addumpdevice`tape`' '이 (가) 발견 되었습니다. 대신 sp_addumpdevice '`disk`'를 사용 하세요. 사용할 때마다 한 번씩 발생합니다.|  
|ALL 권한|GRANT ALL, DENY ALL 또는 REVOKE ALL 구문이 발견된 총 횟수입니다. 특정 권한을 거부하도록 구문을 수정해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|ALTER DATABASE WITH TORN_PAGE_DETECTION|서버 인스턴스가 시작된 이후로 ALTER DATABASE에서 사용되지 않는 기능인 TORN_PAGE_DETECTION 옵션이 사용된 총 횟수입니다. 대신 PAGE_VERIFY 구문을 사용해야 합니다. DDL 문에서 사용할 때마다 한 번씩 발생합니다.|  
|ALTER LOGIN WITH SET CREDENTIAL|사용되지 않는 기능 구문인 ALTER LOGIN WITH SET CREDENTIAL 또는 ALTER LOGIN WITH NO CREDENTIAL이 발견되었습니다. 대신 ADD 또는 DROP CREDENTIAL 구문을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|Azeri_Cyrilllic_90|데이터베이스를 시작하고 데이터 정렬을 사용할 때마다 이벤트가 한 번씩 발생합니다. 이 데이터 정렬을 사용하는 애플리케이션은 수정해야 합니다.|  
|Azeri_Latin_90|데이터베이스를 시작하고 데이터 정렬을 사용할 때마다 이벤트가 한 번씩 발생합니다. 이 데이터 정렬을 사용하는 애플리케이션은 수정해야 합니다.|  
|BACKUP DATABASE 또는 LOG TO TAPE|사용되지 않는 기능인 BACKUP { DATABASE &#124; LOG } TO TAPE 또는 BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_tape*가 발견되었습니다.<br /><br /> 대신 BACKUP { DATABASE &#124; LOG } TO DISK 또는 BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_disk*를 사용하세요. 사용할 때마다 한 번씩 발생합니다.|  
|BACKUP DATABASE 또는 LOG WITH MEDIAPASSWORD|사용되지 않는 기능인 BACKUP DATABASE WITH MEDIAPASSWORD 또는 BACKUP LOG WITH MEDIAPASSWORD가 발견되었습니다. WITH MEDIAPASSWORD는 사용할 수 없습니다.|  
|BACKUP DATABASE 또는 LOG WITH PASSWORD|사용되지 않는 기능인 BACKUP DATABASE WITH PASSWORD 또는 BACKUP LOG WITH PASSWORD가 발견되었습니다. WITH PASSWORD는 사용할 수 없습니다.|  
|COMPUTE [BY]|COMPUTE 또는 COMPUTE BY 구문이 발견되었습니다. ROLLUP에 GROUP BY를 사용하도록 쿼리를 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|CREATE FULLTEXT CATLOG IN PATH|IN PATH가 포함된 CREATE FULLTEXT CATLOG 문이 발견되었습니다. 이 SQL Server 버전에서는 이 절을 사용해도 아무 효과가 없습니다. 사용할 때마다 한 번씩 발생합니다.|  
|CREATE TRIGGER WITH APPEND|WITH APPEND 절이 포함된 CREATE TRIGGER 문이 발견되었습니다. 대신 전체 트리거를 다시 만들어야 합니다. DDL 문에서 사용할 때마다 한 번씩 발생합니다.|  
|CREATE_DROP_DEFAULT|CREATE DEFAULT 또는 DROP DEFAULT 구문이 발견되었습니다. CREATE TABLE 또는 ALTER TABLE에 DEFAULT 옵션을 사용하여 명령을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|CREATE_DROP_RULE|CREATE RULE 구문이 발견되었습니다. 제약 조건을 사용하여 명령을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|데이터 형식: text, ntext 또는 image|`text`, `ntext` 또는 `image` 데이터 형식이 발견되었습니다. `varchar(max)` 데이터 형식을 사용하고 `text`, `ntext` 및 `image` 데이터 형식 구문을 제거하도록 애플리케이션을 다시 작성해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|데이터베이스 호환성 수준 80|데이터베이스가 호환성 수준 80으로 변경된 총 횟수입니다. 다음 릴리스 전에 데이터베이스 및 애플리케이션을 업그레이드하도록 계획합니다. 또한 호환성 수준이 80인 데이터베이스가 시작될 때도 발생합니다.|  
|데이터베이스 호환성 수준 90|데이터베이스가 호환성 수준 90으로 변경된 총 횟수입니다. 이후 릴리스로 데이터베이스 및 애플리케이션을 업그레이드하도록 계획합니다. 또한 호환성 수준이 90인 데이터베이스가 시작될 때도 발생합니다.|  
|DATABASE_MIRRORING|데이터베이스 미러링 기능에 대한 참조가 발견되었습니다. AlwaysOn 가용성 그룹으로 업그레이드하도록 계획하거나 AlwaysOn 가용성 그룹을 지원하지 않는 SQL Server 버전을 실행 중인 경우 로그 전달로 마이그레이션하도록 계획하십시오.|  
|database_principal_aliases|사용되지 않는 sys.database_principal_aliases에 대한 참조가 발견되었습니다. 별칭 대신 역할을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|DATABASEPROPERTY|특정 문이 DATABASEPROPERTY를 참조했습니다. DATABASEPROPERTY 문을 DATABASEPROPERTYEX로 업데이트해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|DATABASEPROPERTYEX('IsFullTextEnabled')|특정 문이 DATABASEPROPERTYEX IsFullTextEnabled 속성을 참조했습니다. 이 속성의 값은 아무런 영향을 주지 않습니다. 사용자 데이터베이스는 전체 텍스트 검색을 사용하도록 항상 설정됩니다. 이 속성은 사용할 수 없습니다. 컴파일마다 한 번씩 발생합니다.|  
|DBCC [UN]PINTABLE|DBCC PINTABLE 또는 DBCC UNPINTABLE 문이 발견되었습니다. 이 문은 아무 효과가 없으며 제거되어야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|DBCC DBREINDEX|DBCC DBREINDEX 문이 발견되었습니다. ALTER INDEX에 REBUILD 옵션을 사용하도록 문을 다시 작성해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|DBCC INDEXDEFRAG|DBCC INDEXDEFRAG 문이 발견되었습니다. ALTER INDEX에 REORGANIZE 옵션을 사용하도록 문을 다시 작성해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|DBCC SHOWCONTIG|DBCC SHOWCONTIG 문이 발견되었습니다. 이 정보를 보려면 sys.dm_db_index_physical_stats를 쿼리해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|기본값으로서 DEFAULT 키워드|DEFAULT 키워드를 기본값으로 사용하는 구문이 발견되었습니다. 사용하지 마십시오. 컴파일마다 한 번씩 발생합니다.|  
|사용되지 않는 암호화 알고리즘|사용되지 않는 암호화 알고리즘 rc4는 다음 버전의 SQL Server에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고 현재 이 기능을 사용하는 애플리케이션은 수정합니다. RC4는 약한 알고리즘이며 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.|  
|DESX 알고리즘|DESX 암호화 알고리즘을 사용하는 문이 발견되었습니다. 암호화에 다른 알고리즘을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|dm_fts_active_catalogs|sys.dm_fts_active_catalogs 뷰의 일부 열이 사용되지 않으므로 dm_fts_active_catalogs 카운터는 항상 0이 됩니다. 사용되지 않는 열을 모니터링하려면 열 관련 카운터(예: dm_fts_active_catalogs.is_paused)를 사용해야 합니다.|  
|dm_fts_active_catalogs.is_paused|[sys.dm_fts_active_catalogs](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql) 동적 관리 뷰의 is_paused 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|dm_fts_active_catalogs.previous_status|sys.dm_fts_active_catalogs 동적 관리 뷰의 previous_status 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|dm_fts_active_catalogs.previous_status_description|sys.dm_fts_active_catalogs 동적 관리 뷰의 previous_status_description 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|dm_fts_active_catalogs.row_count_in_thousands|sys.dm_fts_active_catalogs 동적 관리 뷰의 row_count_in_thousands 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|dm_fts_active_catalogs.status|sys.dm_fts_active_catalogs 동적 관리 뷰의 status 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|dm_fts_active_catalogs.status_description|sys.dm_fts_active_catalogs 동적 관리 뷰의 status_description 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|dm_fts_active_catalogs.worker_count|sys.dm_fts_active_catalogs 동적 관리 뷰의 worker_count 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|dm_fts_memory_buffers|sys.dm_fts_memory_buffers 뷰의 열은 대부분 사용되지 않으므로 dm_fts_memory_buffers 카운터는 항상 0이 됩니다. 사용되지 않는 열을 모니터링하려면 열 관련 카운터(예: dm_fts_memory_buffers.row_count)를 사용해야 합니다.|  
|dm_fts_memory_buffers.row_count|[sys.dm_fts_memory_buffers](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql) 동적 관리 뷰의 row_count 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|두 부분으로 구성된 이름을 사용하는 DROP INDEX|DROP INDEX 구문에 DROP INDEX의 *table_name.index_name* 형식 구문이 포함되었습니다. DROP INDEX 문에서 *index_name* ON *table_name* 구문으로 바꾸세요. 컴파일마다 한 번씩 발생합니다.|  
|EXT_CREATE_ALTER_SOAP_ENDPOINT|FOR SOAP 옵션이 포함된 CREATE 또는 ALTER ENDPOINT 문이 발견되었습니다. 네이티브 XML 웹 서비스는 사용되지 않습니다. 대신 WCF(Windows Communications Foundation) 또는 ASP.NET을 사용해야 합니다.|  
|EXT_endpoint_webmethods|sys.endpoint_webmethods가 발견되었습니다. 네이티브 XML 웹 서비스는 사용되지 않습니다. 대신 WCF(Windows Communications Foundation) 또는 ASP.NET을 사용해야 합니다.|  
|EXT_soap_endpoints|sys.soap_endpoints가 발견되었습니다. 네이티브 XML 웹 서비스는 사용되지 않습니다. 대신 WCF(Windows Communications Foundation) 또는 ASP.NET을 사용해야 합니다.|  
|EXTPROP_LEVEL0TYPE|level0type에서 TYPE이 발견되었습니다. SCHEMA를 level0type으로 사용하고 TYPE을 level1type으로 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|EXTPROP_LEVEL0USER|level1type이 지정된 경우 level0type USER입니다. 사용자에 대한 직접 확장 속성에 대해서만 USER를 level0type으로 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|FASTFIRSTROW|FASTFIRSTROW 구문이 발견되었습니다. OPTION(FAST *n*) 구문을 사용하도록 문을 다시 작성하세요. 컴파일마다 한 번씩 발생합니다.|  
|FILE_ID|FILE_ID 구문이 발견되었습니다. FILE_IDEX를 사용하도록 문을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|fn_get_sql|fn_get_sql 함수가 컴파일되었습니다. sys.dm_exec_sql_text를 대신 사용하십시오. 컴파일마다 한 번씩 발생합니다.|  
|fn_servershareddrives|fn_servershareddrives 함수가 컴파일되었습니다. 대신 sys.dm_io_cluster_shared_drives를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|fn_virtualservernodes|fn_virtualservernodes 함수가 컴파일되었습니다. 대신 sys.dm_os_cluster_nodes를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|fulltext_catalogs|sys.fulltext_catalogs 뷰의 일부 열이 사용되지 않으므로 fulltext_catalogs 카운터는 항상 0이 됩니다. 사용되지 않는 열을 모니터링하려면 해당 열 관련 카운터(예: fulltext_catalogs.data_space_id)를 사용해야 합니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|fulltext_catalogs.data_space_id|[sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql) 카탈로그 뷰의 data_space_id 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|fulltext_catalogs.file_id|sys.fulltext_catalogs 카탈로그 뷰의 file_id 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|fulltext_catalogs.path|sys.fulltext_catalogs 카탈로그 뷰의 path 열이 발견되었습니다. 이 열은 사용할 수 없습니다. 서버 인스턴스에서 이 열에 대한 참조를 발견할 때마다 한 번씩 발생합니다.|  
|FULLTEXTCATALOGPROPERTY('LogSize')|FULLTEXTCATALOGPROPERTY 함수의 LogSize 속성이 발견되었습니다. 이 속성은 사용할 수 없습니다.|  
|FULLTEXTCATALOGPROPERTY('PopulateStatus')|FULLTEXTCATALOGPROPERTY 함수의 PopulateStatus 속성이 발견되었습니다. 이 속성은 사용할 수 없습니다.|  
|FULLTEXTSERVICEPROPERTY('ConnectTimeout')|FULLTEXTSERVICEPROPERTY 함수의 ConnectTimeout 속성이 발견되었습니다. 이 속성은 사용할 수 없습니다.|  
|FULLTEXTSERVICEPROPERTY('DataTimeout')|FULLTEXTSERVICEPROPERTY 함수의 DataTimeout 속성이 발견되었습니다. 이 속성은 사용할 수 없습니다.|  
|FULLTEXTSERVICEPROPERTY('ResourceUsage')|FULLTEXTSERVICEPROPERTY 함수의 ResourceUsage 속성이 발견되었습니다. 이 속성은 사용할 수 없습니다.|  
|GROUP BY ALL|GROUP BY ALL 구문이 발견된 총 횟수입니다. 특정 테이블을 그룹화하도록 구문을 수정해야 합니다.|  
|힌디어|데이터베이스를 시작하고 데이터 정렬을 사용할 때마다 이벤트가 한 번씩 발생합니다. 이 데이터 정렬을 사용하는 애플리케이션은 수정해야 합니다. 대신 Indic_General_90을 사용해야 합니다.|  
|괄호가 없는 HOLDLOCK 테이블 힌트||  
|IDENTITYCOL|INDENTITYCOL 구문이 발견되었습니다. $identity 구문을 사용하도록 문을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|COUNT_BIG(*)이 없는 인덱스 뷰 SELECT 목록|인덱싱된 집계 뷰의 SELECT 목록은 COUNT_BIG(\*)을 포함해야 합니다.|  
|INDEX_OPTION|옵션 주위에 괄호가 없는 CREATE TABLE, ALTER TABLE 또는 CREATE INDEX 구문이 발견되었습니다. 현재 구문을 사용하도록 문을 다시 작성해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|INDEXKEY_PROPERTY|INDEXKEY_PROPERTY 구문이 발견되었습니다. sys.index_columns를 쿼리하도록 문을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|간접 TVF 힌트|뷰를 통해 다중 문 TVF(테이블 반환 함수)를 호출하는 테이블 힌트의 간접 적용은 나중 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거됩니다.|  
|TIMESTAMP 열에 대한 INSERT NULL|TIMESTAMP 열에 NULL 값이 삽입되었습니다. 대신 기본값을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|INSERT_HINTS||  
|Korean_Wansung_Unicode|데이터베이스를 시작하고 데이터 정렬을 사용할 때마다 이벤트가 한 번씩 발생합니다. 이 데이터 정렬을 사용하는 애플리케이션은 수정해야 합니다.|  
|Lithuanian_Classic|데이터베이스를 시작하고 데이터 정렬을 사용할 때마다 이벤트가 한 번씩 발생합니다. 이 데이터 정렬을 사용하는 애플리케이션은 수정해야 합니다.|  
|마케도니아어|데이터베이스를 시작하고 데이터 정렬을 사용할 때마다 이벤트가 한 번씩 발생합니다. 이 데이터 정렬을 사용하는 애플리케이션은 수정해야 합니다. 대신 Macedonian_FYROM_90을 사용해야 합니다.|  
|MODIFY FILEGROUP READONLY|MODIFY FILEGROUP READONLY 구문이 발견되었습니다. READ_ONLY 구문을 사용하도록 문을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|MODIFY FILEGROUP READWRITE|MODIFY FILEGROUP READWRITE 구문이 발견되었습니다. READ_WRITE 구문을 사용하도록 문을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|세 부분 이상으로 구성된 열 이름|쿼리에 열 목록에서 세 부분 또는 네 부분으로 구성된 이름이 사용되었습니다. 표준 호환되는 두 부분으로 구성된 이름을 사용하도록 쿼리를 변경해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|쉼표가 없는 여러 테이블 힌트|테이블 힌트 사이의 구분 기호로 공백이 사용되었습니다. 대신에 쉼표를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|UPDATE 또는 DELETE의 NOLOCK 또는 READUNCOMMITTED|UPDATE 또는 DELETE 문의 FROM 절에서 NOLOCK 또는 READUNCOMMITTED가 발견되었습니다. FROM 절에서 NOLOCK 또는 READUNCOMMITTED 테이블 참고를 제거합니다.|  
|ANSI가 아닌 *= 또는 =\* 외부 조인 연산자|*= 또는 =\* 조인 구문을 사용하는 문이 발견되었습니다. ANSI 조인 구문을 사용하도록 문을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|numbered_stored_procedures||  
|numbered_procedure_parameters|사용되지 않는 sys.numbered_procedure_parameters에 대한 참조가 발견되었습니다. 사용하지 마십시오. 컴파일마다 한 번씩 발생합니다.|  
|numbered_procedures|사용되지 않는 sys.numbered_procedures에 대한 참조가 발견되었습니다. 사용하지 마십시오. 컴파일마다 한 번씩 발생합니다.|  
|이전 스타일의 RAISEERROR|더 이상 사용되지 않는 RAISERROR(형식: RAISERROR 정수 문자열) 구문이 발견되었습니다. 현재 RAISERROR 구문을 사용하여 문을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|임시 연결에 대한 OLEDB|SQLOLEDB는 지원되지 않는 공급자입니다. 임시 연결에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용해야 합니다.|  
|PERMISSIONS|PERMISSIONS 내장 함수에 대한 참조가 발견되었습니다. 대신 sys.fn_my_permissions를 쿼리해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|ProcNums|사용되지 않는 ProcNums 구문이 발견되었습니다. 문을 다시 작성하여 참조를 제거해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|READTEXT|READTEXT 구문이 발견되었습니다. `varchar(max)` 데이터 형식을 사용하고 `text` 데이터 형식 구문을 제거하도록 애플리케이션을 다시 작성해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|RESTORE DATABASE 또는 LOG WITH DBO_ONLY|복원 ... WITH DBO_ONLY 구문이 발견 되었습니다. 복원 사용 ... 대신 RESTRICTED_USER 합니다.|  
|RESTORE DATABASE 또는 LOG WITH MEDIAPASSWORD|복원 ... WITH MEDIAPASSWORD 구문이 발견 되었습니다. WITH MEDIAPASSWORD는 약한 보안 기능을 제공하므로 제거되어야 합니다.|  
|RESTORE DATABASE 또는 LOG WITH PASSWORD|복원 ... WITH PASSWORD 구문이 발견 되었습니다. WITH PASSWORD는 약한 보안 기능을 제공하므로 제거되어야 합니다.|  
|트리거에서 결과 반환|이 이벤트는 트리거를 호출할 때마다 한 번씩 발생합니다. 결과 집합을 반환하지 않도록 트리거를 다시 작성해야 합니다.|  
|ROWGUIDCOL|ROWGUIDCOL 구문이 발견되었습니다. $rowguid 구문을 사용하도록 문을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|SET ANSI_NULLS OFF|SET ANSI_NULLS OFF 구문이 발견되었습니다. 사용되지 않는 이 구문을 제거해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|SET ANSI_PADDING OFF|SET ANSI_PADDING OFF 구문이 발견되었습니다. 사용되지 않는 이 구문을 제거해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|SET CONCAT_NULL_YIELDS_NULL OFF|SET CONCAT_NULL_YIELDS_NULL OFF 구문이 발견되었습니다. 사용되지 않는 이 구문을 제거해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|SET DISABLE_DEF_CNST_CHK|SET DISABLE_DEF_CNST_CHK 구문이 발견되었습니다. 이 구문은 아무 효과가 없습니다. 사용되지 않는 이 구문을 제거해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|SET FMTONLY ON|SET FMTONLY 구문이 발견되었습니다. 사용되지 않는 이 구문을 제거해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|SET OFFSETS|SET OFFSETS 구문이 발견되었습니다. 사용되지 않는 이 구문을 제거해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|SET REMOTE_PROC_TRANSACTIONS|SET REMOTE_PROC_TRANSACTIONS 구문이 발견되었습니다. 사용되지 않는 이 구문을 제거해야 합니다. 대신 연결된 서버 및 sp_serveroption을 사용해야 합니다.|  
|SET ROWCOUNT|DELETE, INSERT 또는 UPDATE 문에서 SET ROWCOUNT 구문이 발견되었습니다. TOP를 사용하여 문을 다시 작성해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|SETUSER|SET USER 문이 발견되었습니다. 대신 EXECUTE AS를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_addapprole|sp_addapprole 프로시저가 발견되었습니다. 대신 CREATE APPLICATION ROLE을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_addextendedproc|sp_addextendedproc 프로시저가 발견되었습니다. 대신 CLR을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_addlogin|sp_addlogin 프로시저가 발견되었습니다. 대신 CREATE LOGIN을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_addremotelogin|sp_addremotelogin 프로시저가 발견되었습니다. 대신 연결된 서버를 사용해야 합니다.|  
|sp_addrole|sp_addrole 프로시저가 발견되었습니다. 대신 CREATE ROLE을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_addserver|sp_addserver 프로시저가 발견되었습니다. 대신 연결된 서버를 사용해야 합니다.|  
|sp_addtype|sp_addtype 프로시저가 발견되었습니다. 대신 CREATE TYPE을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_adduser|sp_adduser 프로시저가 발견되었습니다. 대신 CREATE USER를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_approlepassword|sp_approlepassword 프로시저가 발견되었습니다. 대신 ALTER APPLICATION ROLE을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_attach_db|sp_attach_db 프로시저가 발견되었습니다. 대신 CREATE DATABASE FOR ATTACH를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_attach_single_file_db|sp_single_file_db 프로시저가 발견되었습니다. 대신 CREATE DATABASE FOR ATTACH_REBUILD_LOG를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_bindefault|sp_bindefault 프로시저가 발견되었습니다. 대신 ALTER TABLE 또는 CREATE TABLE의 DEFAULT 키워드를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_bindrule|sp_bindrule 프로시저가 발견되었습니다. 대신 CHECK 제약 조건을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_bindsession|sp_bindsession 프로시저가 발견되었습니다. 대신 MARS(Multiple Active Result Sets) 또는 분산 트랜잭션을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_certify_removable|sp_certify_removable 프로시저가 발견되었습니다. 대신 sp_detach_db를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_changeobjectowner|sp_changeobjectowner 프로시저가 발견되었습니다. 대신 ALTER SCHEMA 또는 ALTER AUTHORIZATION을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_change_users_login|sp_change_users_login 프로시저가 발견되었습니다. 대신 ALTER USER를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'allow updates'|sp_configure의 allow updates 옵션이 발견되었습니다. 시스템 테이블을 더 이상 업데이트할 수 없습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'disallow results from triggers'|sp_configure의 disallow result sets from triggers 옵션이 발견되었습니다. 트리거로부터의 결과 집합을 허용하지 않으려면 sp_configure를 사용하여 옵션을 1로 설정합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'ft crawl bandwidth (max)'|sp_configure의 ft crawl bandwidth (max) 옵션이 발견되었습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'ft crawl bandwidth (min)'|sp_configure의 ft crawl bandwidth (min) 옵션이 발견되었습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'ft notify bandwidth (max)'|sp_configure의 ft notify bandwidth (max) 옵션이 발견되었습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'ft notify bandwidth (min)'|sp_configure의 ft notify bandwidth (min) 옵션이 발견되었습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'locks'|sp_configure의 locks 옵션이 발견되었습니다. 잠금은 더 이상 구성할 수 없습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'open objects'|sp_configure의 open objects 옵션이 발견되었습니다. 열린 개체의 수는 더 이상 구성할 수 없습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'priority boost'|sp_configure의 priority boost 옵션이 발견되었습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다. 대신 Windows start /high ... program.exe 옵션을 사용합니다.|  
|sp_configure의 'remote proc trans'|sp_configure의 remote proc trans 옵션이 발견되었습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_configure의 'set working set size'|sp_configure의 set working set size 옵션이 발견되었습니다. 작업 집합 크기는 더 이상 구성할 수 없습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_control_dbmasterkey_password|sp_control_dbmasterkey_password 저장 프로시저는 마스터 키가 있는지 여부를 확인하지 않습니다. 이전 버전과의 호환성을 위해 허용되지만 경고가 표시됩니다. 이 기능은 더 이상 지원되지 않습니다. 향후 릴리스에서는 마스터 키가 있어야 하며 저장 프로시저 sp_control_dbmasterkey_password에서 사용하는 암호가 데이터베이스 마스터 키를 암호화하는 데 사용된 암호 중 하나와 동일해야 합니다.|  
|sp_create_removable|sp_create_removable 프로시저가 발견되었습니다. 대신 CREATE DATABASE를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_db_vardecimal_storage_format|`vardecimal` 스토리지 형식이 사용되었습니다. 대신 데이터 압축을 사용해야 합니다.|  
|sp_dbcmptlevel|sp_dbcmptlevel 프로시저가 발견되었습니다. ALTER DATABASE 사용 ... 대신 COMPATIBILITY_LEVEL를 설정 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_dbfixedrolepermission|sp_dbfixedrolepermission 프로시저가 발견되었습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_dboption|sp_dboption 프로시저가 발견되었습니다. 대신 ALTER DATABASE 및 DATABASEPROPERTYEX를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_dbremove|sp_dbremove 프로시저가 발견되었습니다. 대신 DROP DATABASE를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_defaultdb|sp_defaultdb 프로시저가 발견되었습니다. 대신 ALTER LOGIN을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_defaultlanguage|sp_defaultlanguage 프로시저가 발견되었습니다. 대신 ALTER LOGIN을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_denylogin|sp_denylogin 프로시저가 발견되었습니다. 대신 ALTER LOGIN DISABLE을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_depends|sp_depends 프로시저가 발견되었습니다. 대신 sys.dm_sql_referencing_entities 및 sys.dm_sql_referenced_entities를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_detach_db \@keepfulltextindexfile|sp_detach_db 문에서 \@keepfulltextindexfile 인수가 발견되었습니다. 이 인수는 사용할 수 없습니다.|  
|sp_dropalias|sp_dropalias 프로시저가 발견되었습니다. 별칭을 사용자 계정 및 데이터베이스 역할의 조합으로 대체해야 합니다. 업그레이드된 데이터베이스에서 sp_dropalias를 사용하여 별칭을 제거해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_dropapprole|sp_dropapprole 프로시저가 발견되었습니다. 대신 DROP APPLICATION ROLE을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_dropextendedproc|sp_dropextendedproc 프로시저가 발견되었습니다. 대신 CLR을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_droplogin|sp_droplogin 프로시저가 발견되었습니다. 대신 DROP LOGIN을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_dropremotelogin|sp_dropremotelogin 프로시저가 발견되었습니다. 대신 연결된 서버를 사용해야 합니다.|  
|sp_droprole|sp_droprole 프로시저가 발견되었습니다. 대신 DROP ROLE을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_droptype|sp_droptype 프로시저가 발견되었습니다. 대신 DROP TYPE을 사용해야 합니다.|  
|sp_dropuser|sp_dropuser 프로시저가 발견되었습니다. 대신 DROP USER를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_estimated_rowsize_reduction_for_vardecimal|`vardecimal` 스토리지 형식이 사용되었습니다. 대신 데이터 압축 및 sp_estimate_data_compression_savings를 사용해야 합니다.|  
|sp_fulltext_catalog|sp_fulltext_catalog 프로시저가 발견되었습니다. 대신 CREATE/ALTER/DROP FULLTEXT CATALOG를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_fulltext_column|sp_fulltext_column 프로시저가 발견되었습니다. 대신 ALTER FULLTEXT INDEX를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_fulltext_database|sp_fulltext_database 프로시저가 발견되었습니다. 대신 ALTER DATABASE를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_fulltext_service \@action=clean_up|sp_fulltext_service 프로시저의 clean_up 옵션이 발견되었습니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_fulltext_service \@action=connect_timeout|sp_fulltext_service 프로시저의 connect_timeout 옵션이 발견되었습니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_fulltext_service \@action=data_timeout|sp_fulltext_service 프로시저의 data_timeout 옵션이 발견되었습니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_fulltext_service \@action=resource_usage|sp_fulltext_service 프로시저의 resource_usage 옵션이 발견되었습니다. 이 옵션은 아무런 기능을 수행하지 않습니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_fulltext_table|sp_fulltext_table 프로시저가 발견되었습니다. 대신 CREATE/ALTER/DROP FULLTEXT INDEX를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_getbindtoken|sp_getbindtoken 프로시저가 발견되었습니다. 대신 MARS(Multiple Active Result Sets) 또는 분산 트랜잭션을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_grantdbaccess|sp_grantdbaccess 프로시저가 발견되었습니다. 대신 CREATE USER를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_grantlogin|sp_grantlogin 프로시저가 발견되었습니다. 대신 CREATE LOGIN을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_help_fulltext_catalog_components|sp_help_fulltext_catalog_components 프로시저가 발견되었습니다. 이 프로시저는 빈 행을 반환하므로 사용할 수 없습니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_help_fulltext_catalogs|sp_help_fulltext_catalogs 프로시저가 발견되었습니다. 대신 sys.fulltext_catalogs를 쿼리해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_help_fulltext_catalogs_cursor|sp_help_fulltext_catalogs_cursor 프로시저가 발견되었습니다. 대신 sys.fulltext_catalogs를 쿼리해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_help_fulltext_columns|sp_help_fulltext_columns 프로시저가 발견되었습니다. 대신 sys.fulltext_index_columns를 쿼리해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_help_fulltext_columns_cursor|sp_help_fulltext_columns_cursor 프로시저가 발견되었습니다. 대신 sys.fulltext_index_columns를 쿼리해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_help_fulltext_tables|sp_help_fulltext_tables 프로시저가 발견되었습니다. 대신 sys.fulltext_indexes를 쿼리해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_help_fulltext_tables_cursor|sp_help_fulltext_tables_cursor 프로시저가 발견되었습니다. 대신 sys.fulltext_indexes를 쿼리해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_helpdevice|sp_helpdevice 프로시저가 발견되었습니다. 대신 sys.backup_devices를 쿼리해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_helpextendedproc|sp_helpextendedproc 프로시저가 발견되었습니다. 대신 CLR을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_helpremotelogin|sp_helpremotelogin 프로시저가 발견되었습니다. 대신 연결된 서버를 사용해야 합니다.|  
|sp_indexoption|sp_indexoption 프로시저가 발견되었습니다. 대신 ALTER INDEX를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_lock|sp_lock 프로시저가 발견되었습니다. 대신 sys.dm_tran_locks를 쿼리해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_password|sp_password 프로시저가 발견되었습니다. 대신 ALTER LOGIN을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_remoteoption|sp_remoteoption 프로시저가 발견되었습니다. 대신 연결된 서버를 사용해야 합니다.|  
|sp_renamedb|sp_renamedb 프로시저가 발견되었습니다. 대신 ALTER DATABASE를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_resetstatus|sp_resetstatus 프로시저가 발견되었습니다. 대신 ALTER DATABASE를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_revokedbaccess|sp_revokedbaccess 프로시저가 발견되었습니다. 대신 DROP USER를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_revokelogin|sp_revokelogin 프로시저가 발견되었습니다. 대신 DROP LOGIN을 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|sp_srvrolepermission|사용되지 않는 sp_srvrolepermission 프로시저가 발견되었습니다. 사용하지 마십시오. 쿼리마다 한 번씩 발생합니다.|  
|sp_unbindefault|sp_unbindefault 프로시저가 발견되었습니다. 대신 CREATE TABLE 또는 ALTER TABLE 문의 DEFAULT 키워드를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sp_unbindrule|sp_unbindrule 프로시저가 발견되었습니다. 규칙 대신 CHECK 제약 조건을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|SQL_AltDiction_CP1253_CS_AS|데이터베이스를 시작하고 데이터 정렬을 사용할 때마다 이벤트가 한 번씩 발생합니다. 이 데이터 정렬을 사용하는 애플리케이션은 수정해야 합니다.|  
|열 별칭으로 사용되는 문자열 리터럴|SELECT 문에서 열 별칭으로 사용되는 문자열이 포함된 구문(예: `'string' = expression`)이 발견되었습니다. 사용하지 마십시오. 컴파일마다 한 번씩 발생합니다.|  
|sys.sql_dependencies|sys.sql_dependencies에 대한 참조가 발견되었습니다. 대신 sys.sql_expression_dependencies를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysaltfiles|sysaltfiles에 대한 참조가 발견되었습니다. 대신 sys.master_files를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|syscacheobjects|syscacheobjects에 대한 참조가 발견되었습니다. 대신 sys.dm_exec_cached_plans, sys.dm_exec_plan_attributes 및 sys.dm_exec_sql_text를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|syscolumns|syscolumns에 대한 참조가 발견되었습니다. 대신 sys.columns를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|syscomments|syscomments에 대한 참조가 발견되었습니다. 대신 sys.sql_modules를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysconfigures|sysconfigures 테이블에 대한 참조가 발견되었습니다. 대신 sys.sysconfigures 뷰를 참조해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysconstraints|sysconstraints에 대한 참조가 발견되었습니다. 대신 sys.check_constraints, sys.default_constraints, sys.key_constraints, sys.foreign_keys를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|syscurconfigs|syscurconfigs에 대한 참조가 발견되었습니다. 대신 sys.configurations를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysdatabases|sysdatabases에 대한 참조가 발견되었습니다. 대신 sys.databases를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysdepends|sysdepends에 대한 참조가 발견되었습니다. 대신 sys.sql_dependencies를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysdevices|sysdevices에 대한 참조가 발견되었습니다. 대신 sys.backup_devices를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysfilegroups|sysfilegroups에 대한 참조가 발견되었습니다. 대신 sys.filegroups를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysfiles|sysfiles에 대한 참조가 발견되었습니다. 대신 sys.database_files를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysforeignkeys|sysforeignkeys에 대한 참조가 발견되었습니다. 대신 sys.foreign_keys를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysfulltextcatalogs|sysfulltextcatalogs에 대한 참조가 발견되었습니다. 대신 sys.fulltext_catalogs를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysindexes|sysindexes에 대한 참조가 발견되었습니다. 대신 sys.indexes, sys.partitions, sys.allocation_units 및 sys.dm_db_partition_stats를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysindexkeys|sysindexkeys에 대한 참조가 발견되었습니다. sys.index_columns를 사용하도록 수정하십시오. 컴파일마다 한 번씩 발생합니다.|  
|syslockinfo|syslockinfo에 대한 참조가 발견되었습니다. 대신 sys.dm_tran_locks를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|syslogins|syslogins에 대한 참조가 발견되었습니다. 대신 sys.server_principals 및 sys.sql_logins를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysmembers|sysmembers에 대한 참조가 발견되었습니다. 대신 sys.database_role_members를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysmessages|sysmessages에 대한 참조가 발견되었습니다. 대신 sys.messages를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysobjects|sysobjects에 대한 참조가 발견되었습니다. 대신 sys.objects를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysoledbusers|sysoledbusers에 대한 참조가 발견되었습니다. 대신 sys.linked_logins를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysopentapes|sysopentapes에 대한 참조가 발견되었습니다. 대신 sys.dm_io_backup_tapes를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysperfinfo|sysperfinfo에 대한 참조가 발견되었습니다. 대신 sys.dm_os_performance_counters를 사용합니다. 컴파일마다 한 번씩 발생합니다.|  
|syspermissions|syspermissions에 대한 참조가 발견되었습니다. 대신 sys.database_permissions 및 sys.server_permissions를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysprocesses|sysprocesses에 대한 참조가 발견되었습니다. 대신 sys.dm_exec_connections, sys.dm_exec_sessions 및 sys.dm_exec_requests를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysprotects|sysprotects에 대한 참조가 발견되었습니다. 대신 sys.database_permissions 및 sys.server_permissions를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysreferences|sysreferences에 대한 참조가 발견되었습니다. 대신 sys.foreign_keys를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysremotelogins|sysremotelogins에 대한 참조가 발견되었습니다. 대신 sys.remote_logins를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysservers|sysservers에 대한 참조가 발견되었습니다. 대신 sys.servers를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|systypes|systypes에 대한 참조가 발견되었습니다. 대신 sys.types를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|sysusers|sysusers에 대한 참조가 발견되었습니다. 대신 sys.database_principals를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|WITH가 없는 테이블 힌트|WITH 키워드 없이 테이블 힌트를 사용한 문이 발견되었습니다. WITH 단어를 포함하도록 문을 수정해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|Text in row 테이블 옵션|'text in row' 테이블 옵션에 대한 참조가 발견되었습니다. 대신 sp_tableoption 'large value types out of row'를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|TEXTPTR|TEXTPTR 함수에 대한 참조가 발견되었습니다. `varchar(max)` 데이터 형식을 사용하고 `text`, `ntext` 및 `image` 데이터 형식 구문을 제거하도록 애플리케이션을 다시 작성해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|TEXTVALID|TEXTVALID 함수에 대한 참조가 발견되었습니다. `varchar(max)` 데이터 형식을 사용하고 `text`, `ntext` 및 `image` 데이터 형식 구문을 제거하도록 애플리케이션을 다시 작성해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|timestamp|사용되지 않는 `timestamp` 데이터 형식이 DDL 문에서 발견된 총 횟수입니다. 대신 `rowversion` 데이터 형식을 사용해야 합니다.|  
|UPDATETEXT 또는 WRITETEXT|UPDATETEXT 또는 WRITETEXT 문이 발견되었습니다. `varchar(max)` 데이터 형식을 사용하고 `text`, `ntext` 및 `image` 데이터 형식 구문을 제거하도록 애플리케이션을 다시 작성해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|USER_ID|USER_ID 함수에 대한 참조가 발견되었습니다. 대신 DATABASE_PRINCIPAL_ID 함수를 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|연결된 서버에 OLEDB 사용||  
|VarDecimal 스토리지 형식|`vardecimal` 스토리지 형식이 사용되었습니다. 대신 데이터 압축을 사용해야 합니다.|  
|XMLDATA|FOR XML 구문이 발견되었습니다. RAW 및 AUTO 모드의 경우 XSD 생성을 사용해야 합니다. EXPLICIT 모드의 경우에는 대체할 옵션이 없습니다. 컴파일마다 한 번씩 발생합니다.|  
|XP_API|확장 저장 프로시저 문이 발견되었습니다. 사용하지 마십시오.|  
|xp_grantlogin|xp_grantlogin 프로시저가 발견되었습니다. 대신 CREATE LOGIN을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
|xp_loginConfig|xp_loginconfig 프로시저가 발견되었습니다. 대신 SERVERPROPERTY의 IsIntegratedSecurityOnly 인수를 사용해야 합니다. 쿼리마다 한 번씩 발생합니다.|  
|xp_revokelogin|xp_revokelogin 프로시저가 발견되었습니다. 대신 ALTER LOGIN DISABLE 또는 DROP LOGIN을 사용해야 합니다. 컴파일마다 한 번씩 발생합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014에서 사용 되지 않는 데이터베이스 엔진 기능](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014에서 사용 되지 않는 전체 텍스트 검색 기능](../search/deprecated-full-text-search-features-in-sql-server-2016.md)   
 [사용 중단 알림 이벤트 클래스](../event-classes/deprecation-announcement-event-class.md)   
 [사용 중단 최종 지원 이벤트 클래스](../event-classes/deprecation-final-support-event-class.md)   
 [SQL Server 2014에서 지원 되지 않는 데이터베이스 엔진 기능](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server 2014에서 지원 되지 않는 전체 텍스트 검색 기능](../../database-engine/discontinued-full-text-search-features-in-sql-server-2014.md)   
 [SQL Server 개체 사용](use-sql-server-objects.md)  
  
  
