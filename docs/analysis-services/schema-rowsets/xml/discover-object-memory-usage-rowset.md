---
title: "DISCOVER_OBJECT_MEMORY_USAGE 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_OBJECT_MEMORY_USAGE rowset
ms.assetid: 211cfa04-7bd6-43fe-8bd5-bfbff78bdafb
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6bfd0d6517f974b60b3d35f25e5836bcd6a7c8e2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="discoverobjectmemoryusage-rowset"></a>DISCOVER_OBJECT_MEMORY_USAGE 행 집합
  개체에서 사용하는 메모리 리소스에 대한 정보를 제공합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_OBJECT_MEMORY_USAGE** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||현재 개체의 부모에 대한 경로입니다.|  
|**OBJECT_ID**|**DBTYPE_WSTR**||개체를 만들 때 정의된 개체 ID입니다.|  
|**OBJECT_MEMORY_SHRINKABLE**|**DBTYPE_I8**||현재 개체가 직접 소유하고 있는 모든 축소 가능 개체에 사용되는 총 메모리 양(바이트)입니다. 현재 개체 소유의 명명된 개체가 소유하고 있는 개체의 메모리는 현재 값에 포함되지 않습니다.|  
|**OBJECT_MEMORY_NONSHRINKABLE**|**DBTYPE_I8**||현재 개체가 직접 소유하고 있는 모든 축소 불가능 개체의 메모리 양(바이트)입니다. 현재 개체 소유의 명명된 개체가 소유하고 있는 개체의 메모리는 현재 값에 포함되지 않습니다.|  
|**OBJECT_VERSION**|**DBTYPE_I4**||개체의 메타데이터 버전 번호로서 개체가 변경될 때마다 변경됩니다.|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||개체 데이터의 계보 번호로서 개체가 처리될 때마다 증가합니다.|  
|**OBJECT_TYPE_ID**|**DBTYPE_I4**||내부 사용을 위해 예약되어 있습니다.|  
|**OBJECT_TIME_CREATED**|**DBTYPE_DBTIMESTAMP**||개체를 만든 시점의 UTC 서버 시간입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_OBJECT_MEMORY_USAGE** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**|(선택 사항)|  
|**OBJECT_ID**|**DBTYPE_WSTR**|선택 사항|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
