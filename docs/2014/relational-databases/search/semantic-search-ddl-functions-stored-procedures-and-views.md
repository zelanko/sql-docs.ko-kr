---
title: 의미 체계 검색 DDL, 함수, 저장 프로시저 및 뷰 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server], database objects
ms.assetid: 182f395f-3168-48a4-b723-ef4403544f9f
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3fcfb35795ac1a5014952d4035690a8254db97c1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082651"
---
# <a name="semantic-search-ddl-functions-stored-procedures-and-views"></a>의미 체계 검색 DDL, 함수, 저장 프로시저 및 뷰
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 통계 의미 체계 검색을 지원하는 Transact-SQL 문 및 데이터베이스 개체를 나열합니다.  
  
 전체 텍스트 검색을 지원하는 문과 데이터베이스 개체의 목록은 [전체 텍스트 검색 DDL, 함수, 저장 프로시저 및 뷰](../views/views.md)를 참조하세요.  
  
##  <a name="ddl"></a> Transact-SQL DDL(데이터 정의 언어) 문  
  
|Object|추가 정보|  
|------------|----------------------|  
|[ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)|[테이블 및 열에 대한 의미 체계 검색 사용](enable-semantic-search-on-tables-and-columns.md)|  
|[CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)|[테이블 및 열에 대한 의미 체계 검색 사용](enable-semantic-search-on-tables-and-columns.md)|  
  
##  <a name="func"></a> 시스템 함수  
  
|Object|추가 정보|  
|------------|----------------------|  
|[semantickeyphrasetable&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql)|[의미 체계 검색을 사용하여 문서에서 키 구 찾기](find-key-phrases-in-documents-with-semantic-search.md)|  
|[semanticsimilaritydetailstable&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)|[의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기](find-similar-and-related-documents-with-semantic-search.md)|  
|[semanticsimilaritytable&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)|[의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기](find-similar-and-related-documents-with-semantic-search.md)|  
  
##  <a name="meta"></a> 시스템 메타데이터 함수  
  
|Object|추가 정보|  
|------------|----------------------|  
|[COLUMNPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)|[테이블 및 열에 대한 의미 체계 검색 사용](enable-semantic-search-on-tables-and-columns.md)|  
|[DATABASEPROPERTYEX&#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql)|[테이블 및 열에 대한 의미 체계 검색 사용](enable-semantic-search-on-tables-and-columns.md)|  
|[FULLTEXTCATALOGPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)|[의미 체계 검색 관리 및 모니터링](manage-and-monitor-semantic-search.md)|  
|[INDEXPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)|[의미 체계 검색 관리 및 모니터링](manage-and-monitor-semantic-search.md)|  
|[OBJECTPROPERTYEX&#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|[테이블 및 열에 대한 의미 체계 검색 사용](enable-semantic-search-on-tables-and-columns.md)|  
|[SERVERPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|[의미 체계 검색 설치 및 구성](install-and-configure-semantic-search.md)|  
  
##  <a name="sproc"></a> 시스템 저장 프로시저  
  
|Object|추가 정보|  
|------------|----------------------|  
|[sp_fulltext_semantic_register_language_statistics_db&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql)|[의미 체계 검색 설치 및 구성](install-and-configure-semantic-search.md)|  
|[sp_fulltext_semantic_unregister_language_statistics_db&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql)|[의미 체계 검색 설치 및 구성](install-and-configure-semantic-search.md)|  
  
##  <a name="cv"></a> 시스템 뷰 - 카탈로그 뷰  
  
|Object|추가 정보|  
|------------|----------------------|  
|[sys.fulltext_index_columns&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|[의미 체계 검색 관리 및 모니터링](manage-and-monitor-semantic-search.md)|  
|[sys.fulltext_semantic_language_statistics_database&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql)|[의미 체계 검색 설치 및 구성](install-and-configure-semantic-search.md)|  
|[sys.fulltext_semantic_languages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql)|[의미 체계 검색 설치 및 구성](install-and-configure-semantic-search.md)|  
  
##  <a name="dmv"></a> 시스템 뷰 - 동적 관리 뷰  
  
|Object|추가 정보|  
|------------|----------------------|  
|[sys.dm_db_fts_index_physical_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)|[의미 체계 검색 관리 및 모니터링](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_index_population&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|[의미 체계 검색 관리 및 모니터링](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_semantic_similarity_population&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)|[의미 체계 검색 관리 및 모니터링](manage-and-monitor-semantic-search.md)|  
  
## <a name="see-also"></a>관련 항목  
 [의미 체계 검색 관리 및 모니터링](manage-and-monitor-semantic-search.md)  
  
  
