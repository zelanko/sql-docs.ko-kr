---
title: 의미 체계 검색 DDL, 함수, 저장 프로시저 및 뷰 | Microsoft 문서
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], database objects
ms.assetid: 182f395f-3168-48a4-b723-ef4403544f9f
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e64481fa28e7aaa2c2cae1b0b44df15eeb9068e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33180969"
---
# <a name="semantic-search-ddl-functions-stored-procedures-and-views"></a>의미 체계 검색 DDL, 함수, 저장 프로시저 및 뷰
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 통계 의미 체계 검색을 지원하는 Transact-SQL 문 및 데이터베이스 개체를 나열합니다.  
  
 전체 텍스트 검색을 지원하는 문과 데이터베이스 개체의 목록은 [전체 텍스트 검색 DDL, 함수, 저장 프로시저 및 뷰](../../relational-databases/search/full-text-search-ddl-functions-stored-procedures-and-views.md)를 참조하세요.  
  
##  <a name="ddl"></a> DDL(데이터 정의 언어) 문:  
  
|Object|추가 정보|  
|------------|----------------------|  
|[ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)|[테이블 및 열에 대한 의미 체계 검색 사용](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
|[CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)|[테이블 및 열에 대한 의미 체계 검색 사용](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
  
##  <a name="func"></a> 시스템 함수  
  
|Object|추가 정보|  
|------------|----------------------|  
|[semantickeyphrasetable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)|[의미 체계 검색을 사용하여 문서에서 키 구 찾기](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)|  
|[semanticsimilaritydetailstable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)|[의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)|  
|[semanticsimilaritytable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)|[의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)|  
  
##  <a name="meta"></a> 시스템 메타데이터 함수  
  
|Object|추가 정보|  
|------------|----------------------|  
|[COLUMNPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)|[테이블 및 열에 대한 의미 체계 검색 사용](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
|[DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)|[테이블 및 열에 대한 의미 체계 검색 사용](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
|[FULLTEXTCATALOGPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)|[의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[INDEXPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)|[의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[OBJECTPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)|[테이블 및 열에 대한 의미 체계 검색 사용](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)|  
|[SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)|[의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)|  
  
##  <a name="sproc"></a> 시스템 저장 프로시저  
  
|Object|추가 정보|  
|------------|----------------------|  
|[sp_fulltext_semantic_register_language_statistics_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md)|[의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)|  
|[sp_fulltext_semantic_unregister_language_statistics_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md)|[의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)|  
  
##  <a name="cv"></a> 카탈로그 뷰  
  
|Object|추가 정보|  
|------------|----------------------|  
|[sys.fulltext_index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|[의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[sys.fulltext_semantic_language_statistics_database&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)|[의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)|  
|[sys.fulltext_semantic_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)|[의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)|  
  
##  <a name="dmv"></a> 동적 관리 뷰  
  
|Object|추가 정보|  
|------------|----------------------|  
|[sys.dm_db_fts_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)|[의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_index_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|[의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_semantic_similarity_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)|[의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)|  
  
## <a name="see-also"></a>참고 항목  
 [의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
