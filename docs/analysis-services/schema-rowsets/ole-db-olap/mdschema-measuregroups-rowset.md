---
title: MDSCHEMA_MEASUREGROUPS 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00748d265b11ea9c97b60428ac3195235efb3f8b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemameasuregroups-rowset"></a>MDSCHEMA_MEASUREGROUPS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  데이터베이스 내의 측정값 그룹을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_MEASUREGROUPS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||이 측정값 그룹이 속한 카탈로그의 이름입니다. 공급자가 카탈로그를 지원하지 않는 경우**NULL** 입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||이 측정값 그룹이 속한 큐브의 이름입니다.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||측정값 그룹의 이름입니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||사람이 읽을 수 있는 멤버 설명입니다.|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**||측정값 그룹이 쓰기 가능한지 여부를 나타내는 부울입니다.<br /><br /> 측정값 그룹이 쓰기 가능하도록 설정된 경우 **true** 를 반환합니다.|  
|**MEASUREGROUP_CAPTION**|**DBTYPE_WSTR**||측정값 그룹의 표시 캡션입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_MEASUREGROUPS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP 스키마 행 집합 용 OLE DB](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
