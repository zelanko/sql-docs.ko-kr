---
title: DISCOVER_OBJECT_MEMORY_USAGE 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bcff047c859bf4e26de8143ed7efef93b8f62e29
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="discoverobjectmemoryusage-rowset"></a>DISCOVER_OBJECT_MEMORY_USAGE 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
