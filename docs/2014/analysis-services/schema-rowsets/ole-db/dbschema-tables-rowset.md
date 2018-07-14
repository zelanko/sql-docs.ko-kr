---
title: DBSCHEMA_TABLES 행 집합 | Microsoft Docs
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
api_name:
- DBSCHEMA_TABLES
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 83537dc9159331342ae344e5003d9c04fd8980eb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211833"
---
# <a name="dbschematables-rowset"></a>DBSCHEMA_TABLES 행 집합
  측정값 그룹 및 차원을 내의 테이블로 표시 된 식별 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DBSCHEMA_TABLES` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|255|이 개체가 속한 카탈로그의 이름입니다.|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|255|이 개체가 속한 큐브의 이름입니다.|  
|`TABLE_NAME`|`DBTYPE_WSTR`|255|`TABLE_TYPE`이 `TABLE`인 경우 개체의 이름입니다.|  
|`TABLE_TYPE`|`DBTYPE_WSTR`||테이블의 유형입니다.<br /><br /> `TABLE` 개체가 측정값 그룹을 나타냅니다.<br /><br /> `SYSTEM TABLE`은 개체가 차원임을 나타냅니다.|  
|`TABLE_GUID`|`DBTYPE_GUID`||지원되지 않습니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||사람이 읽을 수 있는 개체 설명입니다.|  
|`TABLE_PROPID`|`DBTYPE_UI4`||지원되지 않습니다.|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||지원되지 않습니다.|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||개체를 마지막으로 수정한 날짜입니다.|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`||개체의 OLAP 유형입니다.<br /><br /> **MEASURE_GROUP** 개체가 측정값 임을 나타냅니다.<br /><br /> `CUBE_DIMENSION`은 개체가 차원임을 나타냅니다.|  
  
 행 집합은 `TABLE_TYPE`, `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`을 기준으로 정렬됩니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `DBSCHEMA_TABLES` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|선택 사항|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|선택 사항|  
|`TABLE_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`TABLE_TYPE`|`DBTYPE_WSTR`|선택 사항|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`|선택 사항|  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB 스키마 행 집합](ole-db-schema-rowsets.md)  
  
  
