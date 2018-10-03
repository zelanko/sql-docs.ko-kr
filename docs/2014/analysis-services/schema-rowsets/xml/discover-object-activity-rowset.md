---
title: DISCOVER_OBJECT_ACTIVITY 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DISCOVER_OBJECT_ACTIVITY rowset
ms.assetid: 100f7de1-ad5c-4973-b863-3c10df1245c4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8222ba19948adcd65090bfcccaa75b3ddd49a55d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120703"
---
# <a name="discoverobjectactivity-rowset"></a>DISCOVER_OBJECT_ACTIVITY 행 집합
  서비스가 시작된 이후의 개체별 리소스 사용량을 제공합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_OBJECT_ACTIVITY` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`OBJECT_AGGREGATION_HIT`|`DBTYPE_I8`||서비스가 시작된 이후에 개체의 집계가 적중한 횟수입니다.|  
|`OBJECT_AGGREGATION_MISS`|`DBTYPE_I8`||서비스가 시작된 이후에 개체의 기존 집계가 누락된, 즉 사용되지 않은 횟수입니다.|  
|`OBJECT_CPU_TIME_MS`|`DBTYPE_I8`||서비스가 시작된 이후에 개체가 사용한 CPU 시간(밀리초)입니다.|  
|`OBJECT_DATA_VERSION`|`DBTYPE_I4`||개체에 있는 데이터의 계보 번호입니다. 이 번호는 개체가 처리될 때마다 늘어납니다.|  
|`OBJECT_HIT`|`DBTYPE_I8`||서비스가 시작된 이후에 캐시에서 개체가 적중한 횟수입니다.|  
|`OBJECT_ID`|`DBTYPE_WSTR`||개체를 만들 때 정의된 개체 ID입니다.|  
|`OBJECT_MISS`|`DBTYPE_I8`||서비스가 시작된 이후에 캐시에서 개체가 누락된 횟수입니다.|  
|`OBJECT_PARENT_PATH`|`DBTYPE_WSTR`||현재 개체의 부모에 대한 경로입니다.|  
|`OBJECT_READ_KB`|`DBTYPE_I8`||서비스가 시작된 이후에 개체가 읽은 데이터의 누적 값(킬로바이트)입니다.|  
|`OBJECT_READS`|`DBTYPE_I8`||서비스가 시작된 이후에 개체가 수행한 읽기 작업의 누적 수입니다.|  
|`OBJECT_ROWS_RETURNED`|`DBTYPE_I8`||서비스가 시작된 이후에 개체가 호출자에게 반환한 행 수입니다.|  
|`OBJECT_ROWS_SCANNED`|`DBTYPE_I8`||서비스가 시작된 이후에 개체가 검색한 행 수입니다.|  
|`OBJECT_VERSION`|`DBTYPE_I4`||개체의 메타데이터 버전 번호입니다. 이 번호는 개체가 변경될 때마다 변경됩니다.|  
|`OBJECT_WRITE_KB`|`DBTYPE_I8`||서비스가 시작된 이후에 개체가 기록한 데이터의 누적 값(킬로바이트)입니다.|  
|`OBJECT_WRITES`|`DBTYPE_I8`||서비스가 시작된 이후에 개체가 수행한 쓰기 작업의 누적 수입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `DISCOVER_OBJECT_ACTIVTY` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|OBJECT_PARENT_PATH|DBTYPE_WSTR|(선택 사항)|  
|OBJECT_ID|DBTYPE_WSTR|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)  
  
  
