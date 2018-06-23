---
title: DISCOVER_TRACE_DEFINITION_PROVIDERINFO 행 집합 | Microsoft Docs
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
ms.assetid: 8dda2ef7-202a-454b-93f9-a2b29c2d277c
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2f8775ea445a06659fa31f1fee14105525c1414d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092277"
---
# <a name="discovertracedefinitionproviderinfo-rowset"></a>DISCOVER_TRACE_DEFINITION_PROVIDERINFO 행 집합
  추적 공급자의 이름 및 설명과 같은 추적 공급자에 대한 기본 정보를 반환합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_TRACE_DEFINITION_PROVIDERINFO` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`Data`|`DBTYPE_WSTR`|예|공급자 이름, 버전, 빌드 번호 및 설명을 비롯한 추적 공급자를 설명하는 인코딩된 XML 문자열을 포함합니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|A07CCD1B-8148-11D0-87BB-00C04FC33942|  
|ADOMDNAME|TraceDefinitionProviderInfo|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)  
  
  