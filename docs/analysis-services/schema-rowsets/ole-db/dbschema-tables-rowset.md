---
title: "DBSCHEMA_TABLES 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
apiname: DBSCHEMA_TABLES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 89b3d72842621209360980fa18d57ef277f06720
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="dbschematables-rowset"></a>DBSCHEMA_TABLES 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]내의 테이블로 표시 된 차원과 측정값 그룹을 식별 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DBSCHEMA_TABLES** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|255|이 개체가 속한 카탈로그의 이름입니다.|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|255|이 개체가 속한 큐브의 이름입니다.|  
|**TABLE_NAME**|**DBTYPE_WSTR**|255|개체의 이름 경우 **TABLE_TYPE** 은 **테이블**합니다.|  
|**TABLE_TYPE**|**DBTYPE_WSTR**||테이블의 유형입니다.<br /><br /> **테이블** 는 개체가 측정값 그룹 임을 나타냅니다.<br /><br /> **시스템 테이블** 은 개체가 차원 임을 나타냅니다.|  
|**TABLE_GUID**|**DBTYPE_GUID**||지원되지 않습니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||사람이 읽을 수 있는 개체 설명입니다.|  
|**TABLE_PROPID**|**DBTYPE_UI4**||지원되지 않습니다.|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||지원되지 않습니다.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||개체를 마지막으로 수정한 날짜입니다.|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**||개체의 OLAP 유형입니다.<br /><br /> **MEASURE_GROUP** 는 개체가 측정값 그룹 임을 나타냅니다.<br /><br /> **CUBE_DIMENSION** 은 개체가 차원 임을 표시 합니다.|  
  
 에 행 집합은 정렬 **TABLE_TYPE**, **TABLE_CATALOG**, **TABLE_SCHEMA**, 및 **TABLE_NAME**합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DBSCHEMA_TABLES** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|선택 사항|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|선택 사항|  
|**TABLE_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**TABLE_TYPE**|**DBTYPE_WSTR**|선택 사항|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**|선택 사항|  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
