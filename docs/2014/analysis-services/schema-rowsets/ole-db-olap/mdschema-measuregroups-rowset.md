---
title: MDSCHEMA_MEASUREGROUPS 행 집합 | Microsoft Docs
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
api_name:
- MDSCHEMA_MEASUREGROUPS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUPS rowset
ms.assetid: bab1bbd0-421b-4fad-9aee-e6511e0e1f1b
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 046674dc7c579a99e3d9fd90a86c466001c270c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091823"
---
# <a name="mdschemameasuregroups-rowset"></a>MDSCHEMA_MEASUREGROUPS 행 집합
  데이터베이스 내의 측정값 그룹을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `MDSCHEMA_MEASUREGROUPS` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||이 측정값 그룹이 속한 카탈로그의 이름입니다. 공급자가 카탈로그를 지원하지 않을 경우 `NULL`입니다.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||이 측정값 그룹이 속한 큐브의 이름입니다.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||측정값 그룹의 이름입니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||사람이 읽을 수 있는 멤버 설명입니다.|  
|`IS_WRITE_ENABLED`|`DBTYPE_BOOL`||측정값 그룹이 쓰기 가능한지 여부를 나타내는 부울입니다.<br /><br /> 측정값 그룹이 쓰기 가능하도록 설정된 경우 `true`를 반환합니다.|  
|`MEASUREGROUP_CAPTION`|`DBTYPE_WSTR`||측정값 그룹의 표시 캡션입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `MDSCHEMA_MEASUREGROUPS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`CUBE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [OLAP용 OLE DB 스키마 행 집합](ole-db-for-olap-schema-rowsets.md)  
  
  