---
title: MDSCHEMA_INPUT_DATASOURCES 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6efa6baf40c41db7de09ebcb4e5c44990ff7e6ed
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemainputdatasources-rowset"></a>MDSCHEMA_INPUT_DATASOURCES 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  데이터베이스 내에 정의된 데이터 원본을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_INPUT_DATASOURCES** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||이 데이터 원본이 속한 카탈로그의 이름입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**||데이터 원본 개체의 이름입니다.|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**||데이터 원본의 유형입니다. 유효한 값은 다음과 같습니다.<br /><br /> **관계형**<br /><br /> **Olap**|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**||데이터 원본이 만들어진 날짜입니다.|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**||데이터 원본을 마지막으로 수정한 날짜와 시간입니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||동작에 대한 알기 쉬운 설명입니다.|  
|**제한 시간**|**DBTYPE_UI4**||데이터 원본의 제한 시간입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_INPUT_DATASOURCES** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP 스키마 행 집합 용 OLE DB](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
