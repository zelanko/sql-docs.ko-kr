---
title: "MDSCHEMA_HIERARCHIES 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_HIERARCHIES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_HIERARCHIES rowset
ms.assetid: 2e5b2a81-366e-4d5b-af1e-1d372bf596d9
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7ecdc6817c5a2d7e1e88b909080a3156c55f40eb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemahierarchies-rowset"></a>MDSCHEMA_HIERARCHIES 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]특정 차원 내의 각 계층에 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_HIERARCHIES** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|이 계층이 속한 카탈로그의 이름입니다. 공급자가 카탈로그를 지원하지 않는 경우**NULL** 입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|지원되지 않음|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(필수) 이 계층이 속한 큐브의 이름입니다.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|이 계층이 속한 차원의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|**HIERARCHY_NAME**|**DBTYPE_WSTR**|계층 이름입니다. 차원에 단일 계층만 있는 경우 빈칸입니다. 이 값은 항상 한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|계층의 고유한 이름입니다.|  
|**HIERARCHY_GUID**|**DBTYPE_GUID**|지원되지 않음|  
|**HIERARCHY_CAPTION**|**DBTYPE_WSTR**|계층과 연결된 레이블 또는 캡션입니다. 주로 표시 목적으로 사용됩니다. 캡션이 없는 경우 **HIERARCHY_NAME** 반환 됩니다. 차원에 계층이 없거나 단 하나의 계층만 있을 경우 이 열은 차원 이름을 포함합니다.|  
|**DIMENSION_TYPE**|**DBTYPE_I2**|차원의 유형입니다. 유효한 값은 다음과 같습니다.<br /><br /> **MD_DIMTYPE_UNKNOWN** (**0**)<br /><br /> **MD_DIMTYPE_TIME** (**1**)<br /><br /> **MD_DIMTYPE_MEASURE** (**2**)<br /><br /> **MD_DIMTYPE_OTHER** (**3**)<br /><br /> **MD_DIMTYPE_QUANTITATIVE** (**5**)<br /><br /> **MD_DIMTYPE_ACCOUNTS** (**6**)<br /><br /> **MD_DIMTYPE_CUSTOMERS** (**7**)<br /><br /> **MD_DIMTYPE_PRODUCTS** (**8**)<br /><br /> **MD_DIMTYPE_SCENARIO** (**9**)<br /><br /> **MD_DIMTYPE_UTILIY** (**10**)<br /><br /> **MD_DIMTYPE_CURRENCY** (**11**)<br /><br /> **MD_DIMTYPE_RATES** (**12**)<br /><br /> **MD_DIMTYPE_CHANNEL** (**13**)<br /><br /> **MD_DIMTYPE_PROMOTION** (**14**)<br /><br /> **MD_DIMTYPE_ORGANIZATION** (**15**)<br /><br /> **MD_DIMTYPE_BILL_OF_MATERIALS** (**16**)<br /><br /> **MD_DIMTYPE_GEOGRAPHY** (**17**)|  
|**HIERARCHY_CARDINALITY**|**DBTYPE_UI4**|계층의 멤버 수입니다.|  
|**DEFAULT_MEMBER**|**DBTYPE_WSTR**|이 계층의 기본 멤버입니다. 이것은 고유한 이름입니다. 모든 계층에는 기본 멤버가 있어야 합니다.|  
|**ALL_MEMBER**|**DBTYPE_WSTR**|롤업의 가장 높은 수준에 있는 멤버입니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|계층에 대한 사람이 읽을 수 있는 설명입니다. **NULL** 설명이 없는 경우.|  
|**구조**|**DBTYPE_I2**|계층의 구조입니다. 유효한 값은 다음과 같습니다.<br /><br /> **MD_STRUCTURE_FULLYBALANCED** (**0**)<br /><br /> **MD_STRUCTURE_RAGGEDBALANCED** (**1**)<br /><br /> **MD_STRUCTURE_UNBALANCED** (**2**)<br /><br /> **MD_STRUCTURE_NETWORK** (**3**)|  
|**IS_VIRTUAL**|**DBTYPE_BOOL**|항상 반환 **False**합니다.|  
|**IS_READWRITE**|**DBTYPE_BOOL**|Write Back to dimension 열의 사용 여부를 나타내는 부울입니다.<br /><br /> 반환 **TRUE** 경우는 **차원에 쓰기 되돌림** 이 계층 구조를 나타내는 열입니다. 사용 하도록 설정 합니다.|  
|**DIMENSION_UNIQUE_SETTINGS**|**DBTYPE_I4**|항상 반환 **MDDIMENSIONS_MEMBER_KEY_UNIQUE** (**1**).|  
|**DIMENSION_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|항상 반환 **NULL**합니다.|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**|항상 반환 **true**합니다. 차원을 볼 수 없으면 스키마 행 집합에 나타나지 않습니다.|  
|**HIERARCHY_ORDINAL**|**DBTYPE_UI4**|큐브의 모든 차원들 중에서 해당 차원의 서수 번호입니다.|  
|**DIMENSION_IS_SHARED**|**DBTYPE_BOOL**|항상 반환 **TRUE**합니다.|  
|**HIERARCHY_IS_VISIBLE**|**DBTYPE_BOOL**|계층이 표시되는지 여부를 나타내는 부울입니다.<br /><br /> 반환 **TRUE** 계층 구조가 표시 되 고, 그렇지 않으면 **FALSE**합니다.|  
|**HIERARCHY_ORIGIN**|**DBTYPE_UI2**|계층의 원본을 결정하는 비트 마스크입니다.<br /><br /> **MD_USER_DEFINED** 사용자 정의 계층을 식별 하 고 값이 **0x0000001**합니다.<br /><br /> **MD_SYSTEM_ENABLED** 특성 계층을 식별 하 고 값이 **0x0000002**합니다.<br /><br /> **MD_SYSTEM_INTERNAL** 특성 계층이 없는 특성을 식별 하 고 값이 **0x0000004**합니다.<br /><br /> <br /><br /> 부모/자식 특성 계층은 둘 다 **MD_USER_DEFINED** 및 **MD_SYSTEM_ENABLED**합니다.|  
|**HIERARCHY_DISPLAY_FOLDER**|**DBTYPE_WSTR**|사용자 인터페이스에 계층을 표시할 때 사용할 경로입니다. 폴더 이름은 세미콜론(;)으로 구분됩니다. 중첩 된 폴더에 백슬래시가 표시 됩니다 (\\).|  
|**INSTANCE_SELECTION**|**DBTYPE_UI2**|클라이언트 응용 프로그램에 제공하는 계층 표시 방법에 대한 힌트입니다. 유효한 값은 다음과 같습니다.<br /><br /> **MD_INSTANCE_SELECTION_NONE**<br /><br /> **MD_INSTANCE_SELECTION_DROPDOWN**<br /><br /> **MD_INSTANCE_SELECTION_LIST**<br /><br /> **MD_INSTANCE_SELECTION_FILTEREDLIST**<br /><br /> **MD_INSTANCE_SELECTION_MANDATORYFILTER**|  
|**GROUPING_BEHAVIOR**|**DBTYPE_I2**|이 계층에 대한 클라이언트의 예상 그룹화 동작을 지정하는 열거형입니다. 가능한 값은 다음과 같습니다.<br /><br /> **EncourageGrouping** (1)<br /><br /> **DiscourageGrouping** (2)|  
|**STRUCTURE_TYPE**|**DBTYPE_WSTR**|계층의 유형을 나타냅니다. 유효한 값은 다음과 같습니다.<br /><br /> **자연**<br /><br /> **비 자연**<br /><br /> **알 수 없음**|  
  
 에 행 집합은 정렬 **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **DIMENSION_UNIQUE_NAME**, **HIERARCHY_ 이름**합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_HIERARCHIES** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**HIERARCHY_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**HIERARCHY_ORIGIN**|**DBTYPE_UI2**|(선택 사항) 기본 제한은 MD_USER_DEFINED 및 MD_SYSTEM_ENABLED에 적용됩니다.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**HIERARCHY_VISIBILITY**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 Visible<br /><br /> 2 Not visible|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP용 OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
