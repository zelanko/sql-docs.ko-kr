---
title: DISCOVER_MEMORYGRANT 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: d254e42d-9918-47ce-b6df-47f1f0b432dd
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3cae85df7e3c76afd9243771032f21f8f91861f7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229993"
---
# <a name="discovermemorygrant-rowset"></a>DISCOVER_MEMORYGRANT 행 집합
  서버에서 현재 실행 중인 작업에 의해 사용되는 내부 메모리 할당량 부여 목록을 반환합니다. 서버에서 작업이 실행되고 있는지 여부를 확인하려면 `Select * from $System.Discover_Jobs`를 사용합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_MEMORYGRANT` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`MEMORY_ID`|**DBTYPE_I8**||메모리 할당량 부여를 식별하는 번호입니다. 단일 DISCOVER_MEMORYGRANT 요청 컨텍스트에서 고유합니다.|  
|`SPID`|`DBTYPE_I4`|필수|`Select * from $System.Discover_Sessions`를 실행하여 가져올 수 있는 SPID입니다.|  
|`CreationTime`|`DBTYPE_I8 DBTYPE_DBTIMESTAMP`||할당량이 부여된 시간입니다.|  
|`LastRequestTime`|**DBTYPE_DBTIMESTAMP**||할당량 요청을 마지막으로 수정한 시간입니다.|  
|`MemoryUsed`|`DBTYPE_I4`||할당량과의 연결에 사용되는 메모리 양입니다.|  
|`MemoryGranted`|`DBTYPE_I4`||메모리 할당량을 가져오는 작업에 사용하려고 부여되는 메모리 양입니다.|  
|`Blocked`|`DBTYPE_BOOL`||작업의 차단 상태를 나타내는 부울입니다. True이면 작업이 차단되어 다른 작업이 할당량 요청을 부여하기 위해 충분한 할당량을 확보하도록 대기 중임을 나타내고, False이면 작업이 할당량을 수신했으며 실행할 수 있음을 나타냅니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd23-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|MemoryGrant|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)  
  
  
