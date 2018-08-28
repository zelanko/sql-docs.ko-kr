---
title: SQL Server 2016에서 사용되지 않는 전체 텍스트 검색 기능 | Microsoft 문서
ms.custom: ''
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [full-text search]
- full-text search [SQL Server], deprecated features
- full-text queries [SQL Server], proximity
ms.assetid: ab0d799c-ba79-4459-837b-c4862730dafd
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 380465a9bc3aa6d651ed6a47f8e75c94f9d8a5e5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43076585"
---
# <a name="deprecated-full-text-search-features-in-sql-server-2016"></a>SQL Server 2016에서 사용되지 않는 전체 텍스트 검색 기능
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 SQL Server에서 계속 제공되지만 더 이상 사용되지 않는 전체 텍스트 검색 기능에 대해 설명합니다. 이러한 기능은 이후 릴리스에서 제거될 예정입니다. 새 응용 프로그램에서 사용되지 않는 기능은 사용하지 마세요.  
  
**SQL Server:Deprecated Features** 개체 성능 카운터 및 추적 이벤트를 통해 더 이상 사용되지 않는 기능의 사용을 모니터합니다. 자세한 내용은 [SQL Server 개체 사용](../../relational-databases/performance-monitor/use-sql-server-objects.md)을 참조하세요.  
  
## <a name="features-no-longer-supported"></a>더 이상 지원되지 않는 기능  

  
|사용되지 않는 기능|대체 기능|기능 이름|기능 ID|  
|------------------------|-----------------|------------------|----------------|  
|FULLTEXTCATALOGPROPERTY 속성: LogSize|없음|FULLTEXTCATALOGPROPERTY **('LogSize')**|211|  
|FULLTEXTSERVICEPROPERTY 속성:<br /><br /> ConnectTimeout<br /><br /> DataTimeout|없음|FULLTEXTSERVICEPROPERTY **('ConnectTimeout')**<br /><br /> FULLTEXTSERVICEPROPERTY **('DataTimeout'**)|210<br /><br /> 209|  
|sp_fulltext_catalog|CREATE FULL CATALOG<br /><br /> ALTER FULLTEXT CATALOG<br /><br /> DROP FULLTEXT CATALOG|sp_fulltext_catalog|84|  
|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|CREATE FULL INDEX<br /><br /> ALTER FULLTEXT INDEX<br /><br /> DROP FULLTEXT INDEX|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|86<br /><br /> 87<br /><br /> 85|  
|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_tables<br /><br /> sp_help_fulltext_tables_cursor|sys.fulltext_catalogs<br /><br /> sys.fulltext_index_columns<br /><br /> sys.fulltext_indexes|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_table<br /><br /> sp_help_fulltext_tables_cursor|88<br /><br /> 203<br /><br /> 90<br /><br /> 92<br /><br /> 93<br /><br /> 91<br /><br /> 89|  
|sp_fulltext_service 동작 값: clean_up, connect_timeout 및 data_timeout은 0을 반환합니다.|없음|sp_fulltext_service @action=clean_up<br /><br /> sp_fulltext_service @action=connect_timeout<br /><br /> sp_fulltext_service @action=data_timeout|116<br /><br /> 117<br /><br /> 118|  
|sys.dm_fts_active_catalogs 열:<br /><br /> is_paused<br /><br /> previous_status<br /><br /> previous_status_description<br /><br /> row_count_in_thousands<br /><br /> 상태<br /><br /> status_description<br /><br /> worker_count|없음|dm_fts_active_catalogs.is_paused<br /><br /> dm_fts_active_catalogs.previous_status<br /><br /> dm_fts_active_catalogs.previous_status_description<br /><br /> dm_fts_active_catalogs.row_count_in_thousands<br /><br /> dm_fts_active_catalogs.status<br /><br /> dm_fts_active_catalogs.status_description<br /><br /> dm_fts_active_catalogs.worker_count|218<br /><br /> 221<br /><br /> 222<br /><br /> 224<br /><br /> 219<br /><br /> 220<br /><br /> 223|  
|sys.dm_fts_memory_buffers 열:<br /><br /> row_count|없음|dm_fts_memory_buffers.row_count|225|  
|sys.fulltext_catalogs 열:<br /><br /> path<br /><br /> data_space_id<br /><br /> file_id 열|없음|fulltext_catalogs.path<br /><br /> fulltext_catalogs.data_space_id<br /><br /> fulltext_catalogs.file_id|215<br /><br /> 216<br /><br /> 217|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>이후 버전의 SQL Server에서 지원되지 않는 기능  
 아래 전체 텍스트 검색 기능은 다음 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되지만 이후 버전에서는 제거될 예정입니다. 어떤 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 제거될지는 결정되지 않았습니다.  
  
 **기능 이름** 값은 추적 이벤트에는 ObjectName으로 표시되고 성능 카운터 및 sys.dm_os_performance_counters에는 인스턴스 이름으로 표시됩니다. **기능 ID** 값은 추적 이벤트에 ObjectId로 표시됩니다.  
  
|사용되지 않는 기능|대체 기능|기능 이름|기능 ID|  
|------------------------|-----------------|------------------|----------------|  
|CONTAINS 및 CONTAINSTABLE 일반 NEAR 연산자:<br /><br /> {<simple_term> &#124; <prefix_term>}<br /><br /> {<br /><br /> { { NEAR &#124; ~ }    {<simple_term> &#124; <prefix_term>} } [...*n*]<br /><br /> }|사용자 지정 NEAR 연산자:<br /><br /> NEAR(<br /><br /> {   {<simple_term> &#124; <prefix_term>} [ ,…*n* ]<br /><br /> &#124; ( {<simple_term> &#124; <prefix_term>} [,…*n*] )<br /><br /> [,<distance> [,<order>] ]<br /><br /> }<br /><br /> )<br /><br /> <distance> ::= {*integer* &#124; **MAX**}<br /><br /> <order> ::= {TRUE &#124; **FALSE**}|FULLTEXT_OLD_NEAR_SYNTAX|247|  
|CREATE FULLTEXT CATALOG 옵션:<br /><br /> IN PATH '*rootpath*'<br /><br /> ON FILEGROUP *filegroup*|없음|CREATE FULLTEXT CATLOG IN PATH<br /><br /> 없음<sup>*</sup>|237<br /><br /> 없음*|  
|DATABASEPROPERTYEX 속성: IsFullTextEnabled|없음|DATABASEPROPERTYEX **('IsFullTextEnabled')**|202|  
|sp_detach_db 옵션:<br /><br /> [ @keepfulltextindexfile = ] '*KeepFulltextIndexFile*'|없음|sp_detach_db @keepfulltextindexfile|226|  
|sp_fulltext_service 동작 값: resource_usage는 아무 기능도 수행하지 않습니다.|없음|sp_fulltext_service @action=resource_usage|200|  
  
 ***SQL Server:Deprecated Features** 개체는 CREATE FULLTEXT CATLOG ON FILEGROUP *filegroup*의 발생을 모니터링하지 않습니다.  
  
  
