---
title: 전체 텍스트 검색 및 의미 체계 검색 카탈로그 뷰 (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], full-text search
- full-text search [SQL Server], catalog views
- full-text indexes [SQL Server], catalog views
ms.assetid: b08ad2fd-e3d8-458f-96f1-678217e0f419
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ce32b848982bb16155d7f2661bdec0067b984717
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="full-text-search-and-semantic-search-catalog-views-transact-sql"></a>전체 텍스트 검색 및 의미 체계 검색 카탈로그 뷰(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션에서는 전체 텍스트 인덱스 및 의미 체계 인덱스에 대한 정보를 제공하는 카탈로그 뷰에 대해 설명합니다.  
  
## <a name="full-text-search-catalog-views"></a>전체 텍스트 Search 카탈로그 뷰  
 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)  
 각 전체 텍스트 카탈로그에 대해 한 행을 포함합니다.  
  
 [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md)  
 전체 텍스트 인덱싱 작업에 사용할 수 있는 각 문서 유형에 대해 행을 반환합니다. 각 행은 나타냅니다는 **IFilter** SQL Server 인스턴스의에 등록 되어 있는 인터페이스입니다.  
  
 [sys.fulltext_index_catalog_usages](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)  
 전체 텍스트 인덱스 참조에 대한 각 전체 텍스트 카탈로그에 대해 행을 반환합니다.  
  
 [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
 전체 텍스트 인덱스의 일부인 각 열에 대한 행을 포함합니다.  
  
 [sys.fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)  
 전체 텍스트 인덱스를 포함하는 모든 테이블의 각 전체 인덱스 조각에 대한 행이 들어 있습니다.  
  
 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
 테이블 형식 개체의 각 전체 텍스트 인덱스당 한 개의 행을 포함합니다.  
  
 [sys.fulltext_languages](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)  
 SQL Server에 단어 분리기가 등록된 언어당 한 개의 행을 포함합니다. 각 행에는 LCID 및 언어의 이름을 표시합니다.  
  
 [sys.fulltext_stoplists](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
 데이터베이스의 전체 텍스트 중지 목록당 한 개의 행을 포함합니다.  
  
 [sys.fulltext_stopwords](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
 데이터베이스의 모든 중지 목록에 속한 중지 단어당 한 개의 행을 포함합니다.  
  
 [sys.fulltext_system_stopwords](../../relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql.md)  
 시스템 중지 목록에 대한 액세스를 제공합니다.  
  
 [sys.registered_search_properties&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)  
 현재 데이터베이스에서 검색 속성 목록에 있는 각 검색 속성에 대한 행을 포함합니다.  
  
 [sys.registered_search_property_lists&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
 현재 데이터베이스에 각 검색 속성 목록당 한 개의 행을 포함합니다.  
  
## <a name="semantic-search-catalog-views"></a>의미 체계 검색 카탈로그 뷰  
 [sys.fulltext_semantic_language_statistics_database&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에 설치되어 있는 의미 체계 언어 통계 데이터베이스에 대한 행을 반환합니다.  
  
 [sys.fulltext_semantic_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 의미 체계 모델이 등록된 언어마다 하나의 행을 반환합니다. 언어 모델을 등록하면 의미 체계 인덱싱에 해당 언어를 사용하도록 설정됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [전체 텍스트 검색 및 의미 체계 검색 동적 관리 뷰 및 함수 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
