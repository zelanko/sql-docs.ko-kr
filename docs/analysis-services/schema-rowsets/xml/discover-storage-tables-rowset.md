---
title: "DISCOVER_STORAGE_TABLES 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 13df6f10-8efe-4fe9-83a6-96d108809ed1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ceaff6d458686f33a7e32126f3f46c1e5675b144
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="discoverstoragetables-rowset"></a>DISCOVER_STORAGE_TABLES 행 집합
  클라이언트가 테이블 형식 또는 SharePoint 모드에서 실행되는 Analysis Services 데이터베이스에 포함된 테이블을 확인할 수 있도록 합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_STORAGE_TABLES** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|**열 이름**|**유형 표시기**|**길이**|**Description**|  
|---------------------|------------------------|----------------|---------------------|  
|**A S E _**|**DBTYPE_WSTR**||테이블이 포함된 데이터베이스 이름을 지정합니다.<br /><br /> 이 열을 사용하여 **DISCOVER_STORAGE_TABLES** 행 집합을 제한할 수 있습니다. 이 열을 사용하여 행 집합을 제한하지 않은 경우 현재 데이터베이스가 사용됩니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||테이블이 포함된 큐브 또는 모델을 지정합니다.<br /><br /> 이 열을 사용하여 **DISCOVER_STORAGE_TABLES** 행 집합을 제한할 수 있습니다.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**||측정값 그룹의 이름입니다.|  
|**PARTITION_NAME**|**DBTYPE_WSTR**||파티션의 이름입니다.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||차원의 이름입니다.|  
|**TABLE_ID**|**DBTYPE_WSTR**||테이블 특성을 저장하는 데 사용되는 테이블의 ID입니다.|  
|**TABLE_PARTITIONS_COUNT**|**DBTYPE_ WSTR**||테이블 파티션 수입니다.|  
|**HINT_TABLE_TYPE**|**DBTYPE_ WSTR**||테이블 유형의 힌트입니다.|  
|**ROWS_COUNT**|**DBTYPE_UI4**||파티션의 행 수입니다.|  
|**RIVIOLATION_COUNT**|**DBTYPE_UI4**||참조 무결성을 위반하는 행 수입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_STORAGE_TABLES** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|**열 이름**|**유형 표시기**|**제한 상태**|  
|---------------------|------------------------|---------------------------|  
|**A S E _**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|선택 사항|  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 현재 연결되어 있는 기본 데이터베이스에서 저장소 테이블 목록과 각 테이블의 행 수를 반환합니다.  
  
```  
SELECT TABLE_ID, ROWS_COUNT  
FROM $system.DISCOVER_STORAGE_TABLES  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
