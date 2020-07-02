---
title: 전체 텍스트 및 의미 체계 검색 동적 관리 뷰-함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dynamic management objects [SQL Server], full-text search
- full-text search [SQL Server], dynamic management views
ms.assetid: 199dbd5a-29f6-4ef0-8e65-86e32c0aaa3a
author: pmasl
ms.author: pelopes
ms.openlocfilehash: fc289d99e2af7c8bd2f95da742deaf50af128e3a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787039"
---
# <a name="full-text-and-semantic-search-dynamic-management-views---functions"></a>전체 텍스트 및 의미 체계 검색 동적 관리 뷰-함수
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  이 섹션에서는 전체 텍스트 검색 및 의미 체계 검색과 관련된 다음과 같은 동적 관리 뷰 및 함수에 대해 설명합니다.  
  
## <a name="full-text-search-dynamic-management-views-and-functions"></a>전체 텍스트 Search 동적 관리 뷰 및 함수  
 [sys.dm_fts_active_catalogs&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
 서버에서 일부 채우기 작업이 진행 중인 전체 텍스트 카탈로그에 대한 정보를 반환합니다.  
  
 [sys.dm_fts_fdhosts](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
 서버 인스턴스에 있는 필터 데몬 호스트의 현재 작업에 대한 정보를 반환합니다.  
  
 [sys.dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
 지정된 테이블에 대한 전체 텍스트 인덱스 내용에 관한 정보를 반환합니다.  
  
 [sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
 지정된 테이블에 대한 전체 텍스트 인덱스의 문서 수준 내용에 관한 정보를 반환합니다. 지정된 키워드는 여러 문서에 나타날 수 있습니다.  
  
 [sys.dm_fts_index_keywords_by_property](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
 지정된 테이블의 전체 텍스트 인덱스에 있는 속성 관련 내용을 모두 반환합니다. 해당 전체 텍스트 인덱스와 연결된 검색 속성 목록에서 등록한 모든 속성에 속하는 데이터가 모두 여기에 포함됩니다.  
  
 sys.dm_fts_index_keywords_position_by_document  
 문서에서 키워드의 위치를 반환 합니다.  
  
 [sys.dm_fts_index_population](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
 현재 진행 중인 전체 텍스트 인덱스 채우기에 대한 정보를 반환합니다.  
  
 [sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
 전체 텍스트 탐색이나 전체 텍스트 탐색 범위의 일부로 사용되는 특정 메모리 풀에 속한 메모리 버퍼에 대한 정보를 반환합니다.  
  
 [sys.dm_fts_memory_pools](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
 전체 텍스트 탐색이나 전체 텍스트 탐색 범위에 대해 전체 텍스트 Gatherer 구성 요소에서 사용할 수 있는 공유 메모리 풀에 대한 정보를 반환합니다.  
  
 [sys.dm_fts_outstanding_batches](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
 각 전체 텍스트 인덱싱 일괄 처리에 대한 정보를 반환합니다.  
  
 [sys.dm_fts_parser](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
 쿼리 문자열 입력에 지정된 단어 분리기, 동의어 사전 및 중지 목록 조합을 적용한 후 최종 토큰화 결과를 반환합니다. 이 출력은 지정된 쿼리 문자열이 전체 텍스트 엔진에 대해 실행된 경우의 출력과 같습니다.  
  
 [sys.dm_fts_population_ranges](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
 현재 진행 중인 전체 텍스트 인덱스 채우기와 관련된 특정 범위에 대한 정보를 반환합니다.  
  
## <a name="semantic-search-dynamic-management-views-and-functions"></a>의미 체계 검색 동적 관리 뷰 및 함수  
 [sys.dm_fts_semantic_similarity_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
 연결된 의미 체계 인덱스가 있는 각 테이블의 각 유사성 인덱스에 대해 문서 유사성 인덱스 채우기와 관련된 상태 정보가 들어 있는 하나의 행을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;시스템 뷰](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
