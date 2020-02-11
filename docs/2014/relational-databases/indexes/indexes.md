---
title: 인덱스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 58d4d71189598a6fd101e6db0a40b8c8b0a3b903
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63161864"
---
# <a name="indexes"></a>인덱스
  다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용할 수 있는 인덱스 유형을 나열하고 추가 정보에 대한 링크를 제공합니다.  
  
|인덱스 유형|Description|추가 정보|  
|----------------|-----------------|----------------------------|  
|해시|해시 인덱스를 사용하면 메모리의 해시 테이블을 통해 데이터에 액세스할 수 있습니다. 해시 인덱스는 고정된 크기의 메모리를 소모하며, 버킷 수의 함수입니다.|[메모리 액세스에 최적화된 테이블의 인덱스 사용 지침](../in-memory-oltp/memory-optimized-tables.md)|  
|메모리 최적화 비클러스터형 인덱스|메모리 최적화 비클러스터형 인덱스의 경우 메모리 사용은 행 개수 및 인덱스 키 열의 크기를 반영합니다.|[메모리 액세스에 최적화된 테이블의 인덱스 사용 지침](../in-memory-oltp/memory-optimized-tables.md)|  
|클러스터형|클러스터형 인덱스는 클러스터형 인덱스 키에 기반하여 테이블 또는 뷰의 데이터 행을 순서대로 정렬 및 저장합니다. 클러스터형 인덱스는 클러스터형 인덱스 키 값에 기반하여 행의 빠른 검색을 지원하는 B-트리 인덱스 구조로 구현됩니다.|[클러스터형 및 비클러스터형 인덱스 소개](clustered-and-nonclustered-indexes-described.md)<br /><br /> [클러스터형 인덱스 만들기](create-clustered-indexes.md)|  
|비클러스터형 인덱스|비클러스터형 인덱스는 클러스터형 인덱스가 있는 테이블 또는 뷰에 정의하거나 힙에 정의할 수 있습니다. 비클러스터형 인덱스의 각 인덱스 행에는 비클러스터형 키 값과 행 로케이터가 있습니다. 이 로케이터는 클러스터형 인덱스 또는 키 값이 포함된 힙의 데이터 행을 가리킵니다. 인덱스 행은 인덱스 키 값의 순서대로 저장되지만 해당 테이블에 대해 클러스터형 인덱스를 만들지 않으면 데이터 행이 특정 순서대로 정렬되지 않습니다.|[클러스터형 및 비클러스터형 인덱스 소개](clustered-and-nonclustered-indexes-described.md)<br /><br /> [비클러스터형 인덱스 만들기](create-nonclustered-indexes.md)|  
|고유한|고유 인덱스는 인덱스 키에 중복 값을 포함할 수 없으므로 테이블 또는 뷰의 모든 행이 고유합니다.<br /><br /> 고유성은 클러스터형 인덱스와 비클러스터형 인덱스의 속성이 될 수 있습니다.|[고유 인덱스 만들기](create-unique-indexes.md)|  
|columnstore|메모리 내 columnstore 인덱스는 열 기반 데이터 스토리지 및 열 기반 쿼리 처리를 사용하여 데이터를 저장하고 관리합니다.<br /><br /> columnstore 인덱스는 주로 대량 로드 및 읽기 전용 쿼리를 수행하는 데이터 웨어하우징 작업에 효과적입니다. columnstore 인덱스를 사용하면 기존의 행 기반 스토리지보다 최대 **10배의 쿼리 성능** 이익과 압축되지 않은 데이터 크기보다 최대 **7배의 데이터 압축** 을 얻을 수 있습니다.|[Columnstore Indexes Described](columnstore-indexes-described.md)<br /><br /> [비클러스터형 Columnstore 인덱스 사용](../../database-engine/using-nonclustered-columnstore-indexes.md)<br /><br /> [클러스터형 columnstore 인덱스 사용](../../database-engine/using-clustered-columnstore-indexes.md)|  
|포괄 열이 있는 인덱스|키 열과 함께 키가 아닌 열을 포함하도록 확장된 비클러스터형 인덱스입니다.|[포괄 열을 사용하여 인덱스 만들기](create-indexes-with-included-columns.md)|  
|계산 열의 인덱스|하나 이상의 다른 열 또는 특정 결정적 열의 값에서 파생되는 열의 인덱스입니다.|[계산 열의 인덱스](indexes-on-computed-columns.md)|  
|Filtered|특히 데이터의 잘 정의된 하위 집합에서 선택하는 쿼리를 처리하는 데 적합한 최적화된 비클러스터형 인덱스입니다. 이 인덱스에서는 필터 조건자를 사용하여 테이블의 일부 행을 인덱싱합니다. 잘 디자인된 필터링된 인덱스는 전체 테이블 인덱스에 비해 쿼리 성능을 개선하고 인덱스 유지 관리 비용과 인덱스 스토리지 비용을 줄일 수 있습니다.|[필터링된 인덱스 만들기](create-filtered-indexes.md)|  
|공간|공간 인덱스는*geometry*데이터 형식 열의 공간 개체( **공간 데이터** )에서 특정 작업을 보다 효율적으로 수행할 수 있는 기능을 제공합니다. 공간 인덱스는 상대적으로 비용이 많이 드는 공간 작업에서 적용해야 하는 개체 수를 줄여 줍니다.|[공간 인덱스 개요](../spatial/spatial-indexes-overview.md)|  
|XML|
  `xml` 데이터 형식 열의 XML BLOB(Binary Large Object)를 영구적인 단편 형태로 표현한 것입니다.|[XML 인덱스&#40;SQL Server&#41;](../xml/xml-indexes-sql-server.md)|  
|전체 텍스트|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 Microsoft 전체 텍스트 검색 엔진에서 작성 및 유지 관리하는 특수한 유형의 토큰 기반 인덱스입니다. 문자열 데이터에서의 복잡한 단어 검색을 효율적으로 지원합니다.|[전체 텍스트 인덱스 채우기](../search/populate-full-text-indexes.md)|  
  
## <a name="related-tasks"></a>관련 작업  
  
## <a name="related-content"></a>관련 내용  
 [인덱스에 대한 SORT_IN_TEMPDB 옵션](sort-in-tempdb-option-for-indexes.md)  
  
 [인덱스 및 제약 조건 비활성화](disable-indexes-and-constraints.md)  
  
 [인덱스 및 제약 조건 활성화](enable-indexes-and-constraints.md)  
  
 [인덱스 이름 바꾸기](rename-indexes.md)  
  
 [인덱스 옵션 설정](set-index-options.md)  
  
 [인덱스 DDL 작업의 디스크 공간 요구 사항](disk-space-requirements-for-index-ddl-operations.md)  
  
 [인덱스 다시 구성 및 다시 작성](reorganize-and-rebuild-indexes.md)  
  
 [인덱스의 채우기 비율 지정](specify-fill-factor-for-an-index.md)  
  
## <a name="see-also"></a>참고 항목  
 [클러스터형 및 비클러스터형 인덱스 소개](clustered-and-nonclustered-indexes-described.md)  
  
  
