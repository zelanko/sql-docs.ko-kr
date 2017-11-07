---
title: "DISCOVER_MEMORYUSAGE 행 집합 | Microsoft Docs"
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
ms.assetid: e416ea61-9615-468c-a96f-bbf731f803b1
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3dcbb314e1816757562f93290d95a3f9e345460b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="discovermemoryusage-rowset"></a>DISCOVER_MEMORYUSAGE 행 집합
  서버에 의해 할당된 다양한 개체에 대한 DISCOVER_MEMORYUSAGE 통계를 반환합니다.  
  
> [!WARNING]  
>  이 행 집합은 대량의 결과 집합을 생성할 수 있습니다. SQL Server Management Studio가 허용하는 것보다 많은 표시 메모리가 필요해 결과를 표시할 수 없는 경우 다음과 같은 기본 위치의 임시 파일에 결과가 기록됩니다.  
>   
>  '\<드라이브 >: \Users\\< 사용자 이름\>\AppData\Local\Temp\\< fileID\>.xml'.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_MEMORYUSAGE** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MemoryID**|**DBTYPE_UI8**||메모리를 식별 하는 번호입니다.|  
|**MemoryName**|**DBTYPE_WSTR**||메모리를 소유하는 개체의 이름입니다.|  
|**SPID**|**DBTYPE_UI4**|예|메모리를 할당한 세션입니다. 0은 특정 세션에 연결되지 않은 메모리를 나타냅니다.|  
|**CreationTime**|**DBTYPE_DBTIMESTAMP**||"개체가 만들어진 시간"이나 "메모리가 할당된 시간"입니다.|  
|**BaseObjectType**|**DBTYPE_UI4**|예|개체의 유형을 설명하는 숫자입니다. BaseObjectType이 동일한 개체의 유형은 동일합니다.|  
|**MemoryUsed**|**DBTYPE_UI8**|예|개체의 현재 크기로서, 개체에 사용하려고 할당한 메모리보다 작습니다.|  
|**MemoryAllocated**|**DBTYPE_UI8**||개체에 사용하려고 할당한 메모리 양으로서, 개체에 실제로 사용되는 메모리 양보다 큽니다.|  
|**MemoryAllocBase**|**DBTYPE_UI8**||개체 자체에 대해 처음에 할당된 바이트 수입니다(개체 내용에 대한 추가 할당 제외).|  
|**MemoryAllocFromAlloc**|**DBTYPE_UI8**||이 개체의 내용에 대해 할당되는 메모리입니다.|  
|**ElementCount**|**DBTYPE_UI4**||컨테이너 개체의 경우 해당 개체에 포함된 개체 수입니다.|  
|**축소**|**DBTYPE_BOOL**|예|메모리가 축소 가능(메모리 가중으로 인해 삭제 가능)한지 여부를 나타내는 부울입니다. true이면 메모리가 축소 가능하며, false이면 축소 불가능합니다.|  
|**ObjectParentPath**|**DBTYPE_WSTR**||이 개체의 전체 경로를 식별하는 문자열입니다.|  
|**ObjectID**|**DBTYPE_WSTR**||개체를 식별하는 문자열입니다. 이 개체의 전체 경로 문자열에 의해 표시 됩니다: (ObjectParentPath + '.' + ObjectId).|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|A07CCD21-8148-11D0-87BB-00C04FC33942|  
|ADOMDNAME|MemoryUsage|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

