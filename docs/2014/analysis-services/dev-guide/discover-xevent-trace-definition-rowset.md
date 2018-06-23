---
title: DISCOVER_XEVENT_TRACE_DEFINITION 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e1ce2d2d-f994-4318-801a-ee0385aecd84
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2994ce526ff0f8035d16485bf99b146e2366389e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090765"
---
# <a name="discoverxeventtracedefinition-rowset"></a>DISCOVER_XEVENT_TRACE_DEFINITION 행 집합
  서버에서 현재 활성 상태인 XEvent 추적에 대한 정보를 제공합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_XEVENT_TRACE_DEFINITION` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`Data`|`DBTYPE_WSTR`||XEvent 추적의 XML 정의입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd1c-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_XEVENT_TRACE_DEFINITION|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](../schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [SQL Server 확장 이벤트를 사용 하 여 &#40;XEvents&#41; Services 분석을 모니터링 하려면](../instances/monitor-analysis-services-with-sql-server-extended-events.md)   
 [동적 관리 뷰를 사용 하 여 &#40;Dmv&#41; Services 분석을 모니터링 하려면](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  