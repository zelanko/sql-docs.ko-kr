---
title: "DISCOVER_OBJECT_ACTIVITY 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_OBJECT_ACTIVITY rowset
ms.assetid: 100f7de1-ad5c-4973-b863-3c10df1245c4
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fa671c4b9c53d793b9f122d2c7e9eef9d7aac417
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="discoverobjectactivity-rowset"></a>DISCOVER_OBJECT_ACTIVITY 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]서비스의 시작 된 이후의 개체별 리소스 사용량을 제공 합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_OBJECT_ACTIVITY** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_AGGREGATION_HIT**|**DBTYPE_I8**||서비스가 시작된 이후에 개체의 집계가 적중한 횟수입니다.|  
|**OBJECT_AGGREGATION_MISS**|**DBTYPE_I8**||서비스가 시작된 이후에 개체의 기존 집계가 누락된, 즉 사용되지 않은 횟수입니다.|  
|**OBJECT_CPU_TIME_MS**|**DBTYPE_I8**||서비스가 시작된 이후에 개체가 사용한 CPU 시간(밀리초)입니다.|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||개체에 있는 데이터의 계보 번호입니다. 이 번호는 개체가 처리될 때마다 늘어납니다.|  
|**OBJECT_HIT**|**DBTYPE_I8**||서비스가 시작된 이후에 캐시에서 개체가 적중한 횟수입니다.|  
|**OBJECT_ID**|**DBTYPE_WSTR**||개체를 만들 때 정의된 개체 ID입니다.|  
|**OBJECT_MISS**|**DBTYPE_I8**||서비스가 시작된 이후에 캐시에서 개체가 누락된 횟수입니다.|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||현재 개체의 부모에 대한 경로입니다.|  
|**OBJECT_READ_KB**|**DBTYPE_I8**||서비스가 시작된 이후에 개체가 읽은 데이터의 누적 값(킬로바이트)입니다.|  
|**OBJECT_READS**|**DBTYPE_I8**||서비스가 시작된 이후에 개체가 수행한 읽기 작업의 누적 수입니다.|  
|**OBJECT_ROWS_RETURNED**|**DBTYPE_I8**||서비스가 시작된 이후에 개체가 호출자에게 반환한 행 수입니다.|  
|**OBJECT_ROWS_SCANNED**|**DBTYPE_I8**||서비스가 시작된 이후에 개체가 검색한 행 수입니다.|  
|**OBJECT_VERSION**|**DBTYPE_I4**||개체의 메타데이터 버전 번호입니다. 이 번호는 개체가 변경될 때마다 변경됩니다.|  
|**OBJECT_WRITE_KB**|**DBTYPE_I8**||서비스가 시작된 이후에 개체가 기록한 데이터의 누적 값(킬로바이트)입니다.|  
|**OBJECT_WRITES**|**DBTYPE_I8**||서비스가 시작된 이후에 개체가 수행한 쓰기 작업의 누적 수입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_OBJECT_ACTIVTY** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|OBJECT_PARENT_PATH|DBTYPE_WSTR|(선택 사항)|  
|OBJECT_ID|DBTYPE_WSTR|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
