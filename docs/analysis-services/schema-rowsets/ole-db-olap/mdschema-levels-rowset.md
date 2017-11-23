---
title: "MDSCHEMA_LEVELS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
apiname: MDSCHEMA_LEVELS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_LEVELS rowset
ms.assetid: 4313e268-33f4-4e99-96d7-2ec26775c580
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1c0497713e1a115a0c82b7eb957affb82dd060db
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemalevels-rowset"></a>MDSCHEMA_LEVELS 행 집합
  특정 계층 내의 각 수준을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_LEVELS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|이 수준이 속한 카탈로그의 이름입니다. 공급자가 카탈로그를 지원하지 않는 경우**NULL** 입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|이 수준이 속한 스키마 이름입니다. **NULL** 공급자 스키마를 지원 하지 않는 경우.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|이 수준이 속한 큐브 이름입니다.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|이 수준이 속한 차원의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|계층의 고유한 이름입니다. 수준이 둘 이상의 계층에 속한 경우 수준이 속한 각 계층마다 하나의 행이 있습니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|**LEVEL_NAME**|**DBTYPE_WSTR**|수준의 이름입니다.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|수준의 올바르게 이스케이프된 고유한 이름입니다.|  
|**LEVEL_GUID**|**DBTYPE_GUID**|지원되지 않습니다.|  
|**LEVEL_CAPTION**|**DBTYPE_WSTR**|계층과 연결된 레이블 또는 캡션입니다. 주로 표시 목적으로 사용됩니다. 캡션이 없는 경우 **LEVEL_NAME** 반환 됩니다.|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**|계층 루트에서 수준까지의 거리입니다. 루트 수준은 0입니다 (**0)**합니다.|  
|**LEVEL_CARDINALITY**|**DBTYPE_UI4**|수준의 멤버 수입니다.|  
|**LEVEL_TYPE**|**DBTYPE_I4**|수준의 유형입니다.<br /><br /> **MDLEVEL_TYPE_GEO_CONTINENT** (**0x2001**)<br /><br /> **MDLEVEL_TYPE_GEO_REGION** (**0x2002**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTRY** (**0x2003**)<br /><br /> **MDLEVEL_TYPE_GEO_STATE_OR_PROVINCE** (**0x2004**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTY** (**0x2005**)<br /><br /> **MDLEVEL_TYPE_GEO_CITY** (**0x2006**)<br /><br /> **MDLEVEL_TYPE_GEO_POSTALCODE** (**0x2007**)<br /><br /> **MDLEVEL_TYPE_GEO_POINT** (**0x2008**)<br /><br /> **MDLEVEL_TYPE_ORG_UNIT** (**0x1011**)<br /><br /> **MDLEVEL_TYPE_BOM_RESOURCE** (**0x1012**)<br /><br /> **MDLEVEL_TYPE_QUANTITATIVE** (**0x1013**)<br /><br /> **MDLEVEL_TYPE_ACCOUNT** (**0x1014**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER** (**0x1021**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_GROUP** (**0x1022**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_HOUSEHOLD** (**0x1023**)<br /><br /> **MDLEVEL_TYPE_PRODUCT** (**0x1031**)<br /><br /> **MDLEVEL_TYPE_PRODUCT_GROUP** (**0x1032**)<br /><br /> **MDLEVEL_TYPE_SCENARIO** (**0x1015**)<br /><br /> **MDLEVEL_TYPE_UTILITY** (**0x1016**)<br /><br /> **MDLEVEL_TYPE_PERSON** (**0x1041**)<br /><br /> **MDLEVEL_TYPE_COMPANY** (**0x1042**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_SOURCE** (**0x1051**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_DESTINATION** (**0x1052**)<br /><br /> **MDLEVEL_TYPE_CHANNEL** (**0x1061**)<br /><br /> **MDLEVEL_TYPE_REPRESENTATIVE** (**0x1062**)<br /><br /> **MDLEVEL_TYPE_PROMOTION** (**0x1071**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|사람이 읽을 수 있는 수준 설명입니다. 설명이 없는 경우 NULL입니다.|  
|**CUSTOM_ROLLUP_SETTINGS**|**DBTYPE_I4**|사용자 지정 롤업 옵션을 지정하는 비트맵입니다.<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_EXPRESSION** (**0x01**)이이 수준에 대 한 식을 존재 여부를 나타냅니다. (사용되지 않음)<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_COLUMN** (**0x02**)이이 수준에 대 한 사용자 지정 롤업 열 임을 나타냅니다.<br /><br /> **MDLEVELS_SKIPPED_LEVELS** (**0x04**)이 수준의 멤버와 연결 된 건너뛴된 수준이 있음을 나타냅니다.<br /><br /> **MDLEVELS_CUSTOM_MEMBER_PROPERTIES** (**0x08**) 수준의 멤버가 사용자 정의 멤버 속성을가지고 있음을 나타냅니다.<br /><br /> **MDLEVELS_UNARY_OPERATOR** (**0x10**) 수준의 멤버가 단항 연산자를가지고 있음을 나타냅니다.|  
|**LEVEL_UNIQUE_SETTINGS**|**DBTYPE_I4**|고유한 이름 또는 키를 가진 멤버가 해당 수준에만 있는 경우 고유 값을 포함하는 열을 지정하는 비트맵입니다. 이 비트맵에 대해 다음 비트 값 상수가 Msmd.h 파일에 정의됩니다.<br /><br /> **MDDIMENSIONS_MEMBER_KEY_UNIQUE** (**1**)<br /><br /> **MDDIMENSIONS_MEMBER_NAME_UNIQUE** (**2**)<br /><br /> <br /><br /> 키에서 고유는 항상 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. 이름 특성에 설정 되어 있으면 고유 하 게 표시 **UniqueInDimension** 또는 **UniqueInAttribute**|  
|**LEVEL_IS_VISIBLE**|**DBTYPE_BOOL**|수준이 표시되는지 여부를 나타내는 부울입니다.<br /><br /> 항상 True를 반환합니다. 수준을 볼 수 없으면 스키마 행 집합에 포함되지 않습니다.|  
|**LEVEL_ORDERING_PROPERTY**|**DBTYPE_WSTR**|수준의 정렬 기준이 되는 특성의 ID입니다.|  
|**LEVEL_DBTYPE**|**DBTYPE_I4**|**DBTYPE** 수준 특성에 사용 되는 멤버 키 열인의 열거형입니다.<br /><br /> 연결된 키가 멤버 키 열로 사용되는 경우 Null입니다.|  
|**LEVEL_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|항상 NULL을 반환합니다.|  
|**LEVEL_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|수준 멤버 이름의 SQL 표현입니다.|  
|**LEVEL_KEY_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|수준 멤버 키 값의 SQL 표현입니다.|  
|**LEVEL_UNIQUE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|멤버 고유 이름의 SQL 표현입니다.|  
|**LEVEL_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**|수준의 원본을 제공하는 특성 속성의 이름입니다.|  
|**LEVEL_KEY_CARDINALITY**|**DBTYPE_UI2**|수준 키에 있는 열 수입니다.|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|수준의 원본이 지정된 방식을 정의하는 비트맵입니다.<br /><br /> **MD_ORIGIN_USER_DEFINED** 사용자 정의 계층의 수준을 식별 합니다.<br /><br /> **MD_ORIGIN_ATTRIBUTE** 특성 계층의 수준을 식별 합니다.<br /><br /> **MD_ORIGIN_KEY_ATTRIBUTE** 키 특성 계층의 수준을 식별 합니다.<br /><br /> **MD_ORIGIN_INTERNAL** 활성화 되지 않은 특성 계층의 수준을 식별 합니다.|  
  
 에 행 집합은 정렬 **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **DIMENSION_UNIQUE_NAME**, **HIERARCHY_ UNIQUE_NAME**, **LEVEL_NUMBER**합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_LEVELS** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**LEVEL_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|(선택 사항) 기본 제한에 적용은 **MD_USER_DEFINED** 및 **MD_SYSTEM_ENABLED**|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**LEVEL_VISIBILITY**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 다음 값 중 하나를 사용 하 여 비트맵:<br /><br /> 1 Visible<br /><br /> 2 Not visible|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP용 OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
