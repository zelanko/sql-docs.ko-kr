---
description: 전체 텍스트 검색 및 의미 체계 검색 저장 프로시저(Transact-SQL)
title: 전체 텍스트 검색 및 의미 체계 검색 저장 프로시저 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], stored procedures
- full-text search [SQL Server], stored procedures
- full-text catalogs [SQL Server], stored procedures
- system stored procedures [SQL Server], full-text search
ms.assetid: 0d185a16-2b16-4958-884f-efe675e2e551
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0edf572ad6ae1e94455abcdba60286b0c6664254
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481637"
---
# <a name="full-text-search-and-semantic-search-stored-procedures-transact-sql"></a>전체 텍스트 검색 및 의미 체계 검색 저장 프로시저(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 전체 텍스트 인덱스 및 의미 체계 인덱스를 구현 하 고 쿼리 하는 데 사용 되는 다음과 같은 시스템 저장 프로시저를 지원 합니다.  
  
## <a name="full-text-search-stored-procedures"></a>전체 텍스트 검색 저장 프로시저  
 [sp_fulltext_catalog](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)  
 전체 텍스트 카탈로그를 만들고 삭제하며, 해당 카탈로그에 대한 인덱싱 동작을 시작하고 중지합니다. 각 데이터베이스에 여러 개의 전체 텍스트 카탈로그를 만들 수 있습니다.  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)][전체 텍스트 카탈로그 만들기](../../t-sql/statements/create-fulltext-catalog-transact-sql.md), [전체 텍스트 카탈로그 변경](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)및 [전체 텍스트 카탈로그 삭제](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) 를 사용 합니다.  
  
 [sp_fulltext_column](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)  
 테이블의 특정 열을 전체 텍스트 인덱싱에 참여시킬지 여부를 지정합니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [ALTER 전체 인덱스](../../t-sql/statements/alter-fulltext-index-transact-sql.md) 를 사용 해야 합니다.  
  
 [sp_fulltext_database](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그에 영향을 미치지 않으며 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)  
 문서 식별자 (**DocId**)와 전체 텍스트 키 값 간의 매핑을 반환 합니다.  
  
 [sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 LCID에 해당하는 업데이트된 동의어 사전 파일의 데이터를 구문 분석하고 로드하며 이 동의어 사전 파일을 사용하는 전체 텍스트 쿼리의 다시 컴파일을 유발합니다.  
  
 [sp_fulltext_pendingchanges](../../relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql.md)  
 변경 내용 추적을 사용하는 지정된 테이블에 대해 보류 중인 삽입, 업데이트, 삭제 등의 처리되지 않은 변경 내용을 반환합니다.  
  
 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
 SQL Server의 전체 텍스트 검색의 서버 속성을 변경합니다.  
  
 [sp_fulltext_table](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)  
 테이블을 전체 텍스트 인덱싱에 표시하거나 표시하지 않습니다.  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md), [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)및 [DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md) 를 사용하십시오.  
  
 [sp_help_fulltext_catalog_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql.md)  
 현재 데이터베이스의 모든 전체 텍스트 카탈로그에 사용된 필터, 단어 분리기, 프로토콜 처리기 등 모든 구성 요소의 목록을 반환합니다.  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_help_fulltext_catalogs](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
 지정된 전체 텍스트 카탈로그에 대해 전체 텍스트 인덱싱된 테이블의 ID, 이름, 루트 디렉터리, 상태 및 번호를 반환합니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) 카탈로그 뷰를 사용 하십시오.  
  
 [sp_help_fulltext_catalogs_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)  
 커서를 사용하여 지정된 전체 텍스트 카탈로그에 대해 전체 텍스트 인덱싱된 테이블의 ID, 이름, 루트 디렉터리, 상태 및 번호를 반환할 수 있습니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) 카탈로그 뷰를 사용 하십시오.  
  
 [sp_help_fulltext_columns](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)  
 전체 텍스트 인덱싱하기 위해 지정한 열을 반환합니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) 카탈로그 뷰를 사용 하십시오.  
  
 [sp_help_fulltext_columns_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)  
 커서를 사용하여 전체 텍스트 인덱싱에 등록된 열을 반환할 수 있습니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) 카탈로그 뷰를 사용 하십시오.  
  
 [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
 등록된 단어 분리기, 필터 및 프로토콜 처리기에 대한 정보와 함께 지정된 구성 요소를 사용한 전체 텍스트 카탈로그 및 데이터베이스 식별자 목록을 반환합니다.  
  
 [sp_help_fulltext_tables](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)  
 전체 텍스트 인덱싱용으로 등록된 테이블의 목록을 반환합니다.  
  
 [sp_help_fulltext_tables_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)  
 전체 텍스트 인덱싱용으로 등록된 테이블의 목록을 반환합니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md) 카탈로그 뷰를 사용 하십시오.  
  
## <a name="semantic-search-stored-procedures"></a>의미 체계 검색 저장 프로시저  
 [sp_fulltext_semantic_register_language_statistics_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에서 미리 채워진 의미 체계 언어 통계 데이터베이스를 등록합니다.  
  
 [sp_fulltext_semantic_unregister_language_statistics_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md)  
 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 기존 의미 체계 언어 통계 데이터베이스의 등록을 취소하고 연결된 모든 메타데이터를 삭제합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;전체 텍스트 검색 및 의미 체계 검색 카탈로그 뷰 ](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)   
 [Transact-sql&#41;전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)  
  
  
