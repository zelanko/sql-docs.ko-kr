---
title: "MDSCHEMA_MEMBERS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_MEMBERS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_MEMBERS rowset
ms.assetid: 0b1aada0-67f8-4ef6-81b2-0100b65e0c2f
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8ee6e7231d4a3a3696de68e3c22b8cad7eb05a92
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemamembers-rowset"></a>MDSCHEMA_MEMBERS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]데이터베이스 내의 멤버에 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_MEMBERS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||이 멤버가 속한 데이터베이스 이름입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||이 멤버가 속한 스키마 이름입니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||이 멤버가 속한 큐브 이름입니다.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||이 멤버가 속한 차원의 고유한 이름입니다.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||이 멤버가 속한 계층의 고유한 이름입니다.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||이 멤버가 속한 수준의 고유한 이름입니다.|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**||계층 루트에서 멤버까지의 거리입니다. 루트 수준은 0입니다.|  
|**MEMBER_ORDINAL**|**DBTYPE_UI4**||(사용 되지 않음) 항상 반환 **0**합니다.|  
|**MEMBER_NAME**|**DBTYPE_WSTR**||멤버의 이름입니다.|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||멤버의 고유한 이름입니다.|  
|**MEMBER_TYPE**|**DBTYPE_I4**||멤버의 유형입니다.<br /><br /> **MDMEMBER_TYPE_UNKNOWN** (**0**)<br /><br /> **MDMEMBER_TYPE_REGULAR** (**1**)<br /><br /> **MDMEMBER_TYPE_ALL** (**2**)<br /><br /> **MDMEMBER_TYPE_MEASURE** (**3**)<br /><br /> **MDMEMBER_TYPE_FORMULA** (**4**)<br /><br /> <br /><br /> Note를 <br />                    **MDMEMBER_TYPE_FORMULA**우선 **MDMEMBER_TYPE_MEASURE**합니다. 예를 들어, Measures 차원에 수식 (계산된) 멤버가 없는 경우 없으면으로 **MDMEMBER_TYPE_FORMULA**합니다.|  
|**MEMBER_GUID**|**DBTYPE_GUID**||멤버의 GUID입니다. **NULL** GUID가 없는 경우.|  
|**MEMBER_CAPTION**|**DBTYPE_WSTR**||멤버에 연결된 레이블 또는 캡션입니다. 주로 표시 목적으로 사용됩니다. 캡션이 없는 경우 **MEMBER_NAME** 반환 됩니다.|  
|**CHILDREN_CARDINALITY**|**DBTYPE_UI4**||멤버의 자식 수입니다. 예상치일 수 있으므로 사용자는 이 값을 정확한 개수로 간주하면 안 됩니다. 공급자는 가능한 한 최적의 예상치를 반환해야 합니다.|  
|**PARENT_LEVEL**|**DBTYPE_UI4**||계층 루트 수준에서 멤버 부모까지의 거리입니다. 루트 수준은 0입니다.|  
|**PARENT_UNIQUE_NAME**|**DBTYPE_WSTR**||멤버 부모의 고유한 이름입니다. 루트 수준의 모든 멤버에 대해서**NULL** 이 반환됩니다.|  
|**PARENT_COUNT**|**DBTYPE_UI4**||이 멤버에 있는 부모 수입니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||이 열은 항상 반환 된 **NULL** 값입니다.<br /><br /> 이 열은 이전 버전과의 호환성을 위한 것입니다.|  
|**식**|**DBTYPE_WSTR**||식 계산의 경우 형식의 멤버가 없으면 **MDMEMBER_TYPE_FORMULA**합니다.|  
|**MEMBER_KEY**|**DBTYPE_WSTR**||멤버의 키 열 값입니다. 반환 **NULL** 멤버의 복합 키입니다.|  
|**IS_PLACEHOLDERMEMBER**|**DBTYPE_BOOL**||멤버가 차원 계층에서 빈 위치에 대한 자리 표시자 멤버인지 여부를 나타내는 부울입니다.<br /><br /> 유효한 경우에만 **MDX Compatibility** 속성이 2로 설정 되어 있습니다.|  
|**IS_DATAMEMBER**|**DBTYPE_BOOL**||멤버가 데이터 멤버인지 여부를 나타내는 부울입니다.<br /><br /> 멤버가 데이터 멤버인 경우 True를 반환합니다.|  
|**범위**|**DBTYPE_I4**||멤버의 범위입니다. 멤버는 세션 계산 멤버이거나 전역 계산 멤버일 수 있습니다. 열을 반환 **NULL** 비계산 멤버에 대 한 합니다. 이 열 값은 다음 중 하나일 수 있습니다.<br /><br /> MDMEMBER_SCOPE_GLOBAL=1<br /><br /> MDMEMBER_SCOPE_SESSION=2|  
|**0 개 이상의 추가 열**|**DBTYPE_UI2**||멤버가 여러 수준에서 반환될 수 있는 경우에는 속성이 반환되지 않습니다. 예를 들어, Tree 연산자가 **부모** 및 **자체** 부모-자식 계층에 대 한 멤버 속성이 반환 되지 않습니다.<br /><br /> 이 열은 이전 수준에 구멍이 있고 멤버의 부모가 요청되는 경우와 같이 Tree 연산자에서 여러 수준의 멤버가 반환될 수 있는 비정형 계층에 적용됩니다.|  
  
 에 행 집합은 정렬 **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **DIMENSION_UNIQUE_NAME**, **HIERARCHY_ UNIQUE_NAME**, **LEVEL_UNIQUE_NAME**, **LEVEL_NUMBER**, **MEMBER_ORDINAL**합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_MEMBERS** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**|(선택 사항)|  
|**MEMBER_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**MEMBER_CAPTION**|**DBTYPE_WSTR**|(선택 사항)|  
|**MEMBER_TYPE**|**DBTYPE_I4**|(선택 사항)|  
|**TREE_OP**|**DBTYPE_I4**|단일 멤버에만 적용됩니다(선택 사항).<br /><br /> **MDTREEOP_ANCESTORS** (**0x20**) 모든 상위 항목을 반환 합니다.<br /><br /> **MDTREEOP_CHILDREN** (**0x01**)은 인접 자식만 반환 합니다.<br /><br /> **MDTREEOP_SIBLINGS** (**0x02**) 동일한 수준의 멤버를 반환 합니다.<br /><br /> **MDTREEOP_PARENT** (**0x04**)은 인접 부모만 반환 합니다.<br /><br /> **MDTREEOP_SELF** (**0x08**) 자체 반환 된 행의 목록에 반환 합니다.<br /><br /> **MDTREEOP_DESCENDANTS** (**0x10**) 모든 하위 항목을 반환 합니다.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP용 OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
