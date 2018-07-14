---
title: 전체 텍스트 검색 DDL, 함수, 저장 프로시저 및 뷰 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 98c36715-4195-482e-a4a3-d93ff65b75f1
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cd955394028c3a748e4a7e6b1e5a24f9013ef79e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277459"
---
# <a name="full-text-search-ddl-functions-stored-procedures-and-views"></a>전체 텍스트 검색 DDL, 함수, 저장 프로시저 및 뷰
  속성 검색 기능을 포함하여 전체 텍스트 검색을 지원하는 Transact-SQL 문 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체를 나열합니다.  
  
 사용되지 않는 개체는 이 목록에 포함되지 않습니다.  
  
 의미 체계 검색을 지원하는 데이터베이스 개체 목록은 [Semantic Search DDL, Functions, Stored Procedures, and Views](../views/views.md)를 참조하세요.  
  
##  <a name="ddl"></a> Transact-SQL DDL(데이터 정의 언어) 문  
  
-   [CREATE FULLTEXT CATALOG&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
-   [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
-   [CREATE FULLTEXT STOPLIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)  
  
-   [CREATE SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql)  
  
-   [ALTER FULLTEXT CATALOG&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)  
  
-   [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
-   [ALTER FULLTEXT STOPLIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)  
  
-   [ALTER SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql)  
  
-   ["DROP FULLTEXT CATALOG&#40;Transact-SQL&#41;"](/sql/t-sql/statements/drop-fulltext-catalog-transact-sql)  
  
-   [DROP FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-index-transact-sql)  
  
-   [DROP FULLTEXT STOPLIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
-   [DROP SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-search-property-list-transact-sql)  
  
##  <a name="func"></a> 시스템 조건자 및 함수  
  
-   [CONTAINS&#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
-   [CONTAINSTABLE&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)  
  
-   [FREETEXT&#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)  
  
-   [FREETEXTTABLE&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)  
  
##  <a name="meta"></a> 시스템 메타데이터 함수  
  
-   [COLUMNPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)  
  
-   [FULLTEXTCATALOGPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)  
  
-   [FULLTEXTSERVICEPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextserviceproperty-transact-sql)  
  
-   [INDEXPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)  
  
-   [OBJECTPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/objectpropertyex-transact-sql)  
  
-   [OBJECTPROPERTYEX&#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)  
  
-   [SERVERPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
  
##  <a name="proc"></a> 시스템 저장 프로시저  
  
-   [sp_fulltext_keymappings&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql)  
  
-   [sp_fulltext_load_thesaurus_file&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql)  
  
-   [sp_fulltext_pendingchanges&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql)  
  
-   [sp_fulltext_service&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)  
  
-   [sp_help_fulltext_system_components&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql)  
  
##  <a name="cat"></a> 시스템 뷰 - 카탈로그 뷰  
  
-   [sys.fulltext_catalogs&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql)  
  
-   [sys.fulltext_document_types&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql)  
  
-   [sys.fulltext_index_catalog_usages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql)  
  
-   [sys.fulltext_index_columns&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
-   [sys.fulltext_index_fragments&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql)  
  
-   [sys.fulltext_indexes&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql)  
  
-   [sys.fulltext_languages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)  
  
-   [sys.fulltext_stoplists&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
-   [sys.fulltext_stopwords&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)  
  
-   [sys.fulltext_system_stopwords&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql)  
  
-   [sys.registered_search_properties&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql)  
  
-   [sys.registered_search_property_lists&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
##  <a name="dmv"></a> 시스템 뷰 - 동적 관리 뷰  
  
-   [sys.dm_fts_active_catalogs&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql)  
  
-   [sys.dm_fts_fdhosts&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql)  
  
-   [sys.dm_fts_index_keywords&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql)  
  
-   [sys.dm_fts_index_keywords_by_document&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql)  
  
-   [sys.dm_fts_index_keywords_by_property&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql)  
  
-   [sys.dm_fts_index_population&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)  
  
-   [sys.dm_fts_memory_buffers&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)  
  
-   [sys.dm_fts_memory_pools&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql)  
  
-   [sys.dm_fts_outstanding_batches&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql)  
  
-   [sys.dm_fts_parser&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
-   [sys.dm_fts_population_ranges&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql)  
  
  
