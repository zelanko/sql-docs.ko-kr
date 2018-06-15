---
title: MDSCHEMA_PROPERTIES 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7cccd5d28d3f4d2675229929a2bf3d35b383a032
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036824"
---
# <a name="mdschemaproperties-rowset"></a>MDSCHEMA_PROPERTIES 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  데이터베이스 내의 멤버 속성을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_PROPERTIES** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||데이터베이스의 이름입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||이 속성이 속한 스키마 이름입니다. **NULL** 공급자 스키마를 지원 하지 않는 경우.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||큐브의 이름입니다.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||차원의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||계층의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||이 속성이 속한 수준의 고유한 이름입니다. 반환 해야 하는 경우 공급자는 명명 된 수준을 지원 하지 않습니다는 **DIMENSION_UNIQUE_NAME** 이 필드에 대 한 값입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||속성이 속한 멤버의 고유한 이름입니다. 명명된 수준을 지원하지 않거나 멤버별 기준으로 속성을 보유하는 데이터 저장소에 사용됩니다. 속성 구조의 모든 멤버에 적용 되는 경우이 열은 **NULL**합니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|**PROPERTY_TYPE**|**DBTYPE_I2**||속성의 유형을 지정하는 비트맵입니다.<br /><br /> **MDPROP_MEMBER** (**1**) 멤버의 속성을 식별 합니다. 이 속성은 SELECT 문의 DIMENSION PROPERTIES 절에 사용할 수 있습니다.<br /><br /> **MDPROP_CELL** (**2**)-셀의 속성을 식별 합니다. 이 속성은 SELECT 문의 끝에 나오는 CELL PROPERTIES 절에 사용할 수 있습니다.<br /><br /> **MDPROP_SYSTEM** (**4**) 내부 속성을 식별 합니다.<br /><br /> **MDPROP_BLOB** (**8**) 이진 대형 개체 (blob)을 포함 하는 속성을 식별 합니다.|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**||속성의 이름입니다. 속성에 대 한 키 속성에 대 한 이름으로 동일한 경우 **PROPERTY_NAME** 비어 있게 됩니다.|  
|**PROPERTY_CAPTION**|**DBTYPE_WSTR**||주로 표시용으로 사용되는, 속성에 연결된 레이블 또는 캡션입니다. 반환 **PROPERTY_NAME** 캡션을 존재 하지 않는 경우.|  
|**DATA_TYPE**|**DBTYPE_UI2**||속성의 데이터 형식.|  
|**때**|**DBTYPE_UI4**||속성이 문자, 이진 또는 비트 유형인 경우 속성에 사용할 수 있는 최대 길이입니다.<br /><br /> 0 값은 정의된 최대 길이가 없음을 나타냅니다.<br /><br /> 반환 **NULL** 다른 모든 데이터 형식에 대 한 합니다.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||속성이 문자 또는 이진 유형인 경우 속성에 사용할 수 있는 최대 길이(바이트)입니다.<br /><br /> 0 값은 정의된 최대 길이가 없음을 나타냅니다.<br /><br /> 반환 **NULL** 다른 모든 데이터 형식에 대 한 합니다.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||속성이 숫자 데이터 형식인 경우 속성의 최대 전체 자릿수입니다.<br /><br /> 반환 **NULL** 다른 모든 데이터 형식에 대 한 합니다.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||소수점 경우의 오른쪽에 있는 자릿수는 **DBTYPE_NUMERIC** 또는 **DBTYPE_DECIMAL** 유형입니다.<br /><br /> 반환 **NULL** 다른 모든 데이터 형식에 대 한 합니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||사람이 읽을 수 있는 속성 설명입니다. **NULL** 설명이 없는 경우.|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**||속성의 형식입니다. 다음 열거 중 하나일 수 있습니다.<br /><br /> **MD_PROPTYPE_REGULAR** (**0x00**)<br /><br /> **MD_PROPTYPE_ID** (**0x01**)<br /><br /> **MD_PROPTYPE_RELATION_TO_PARENT** (**0x02**)<br /><br /> **MD_PROPTYPE_ROLLUP_OPERATOR** (**0x03**)<br /><br /> **MD_PROPTYPE_ORG_TITLE** (**0x11**)<br /><br /> **MD_PROPTYPE_CAPTION** (**0x21**)<br /><br /> **MD_PROPTYPE_CAPTION_SHORT** (**0x22**)<br /><br /> **MD_PROPTYPE_CAPTION_DESCRIPTION** (**0x23**)<br /><br /> **MD_PROPTYPE_CAPTION_ABREVIATION** (**0x24**)<br /><br /> **MD_PROPTYPE_WEB_URL** (**0x31**)<br /><br /> **MD_PROPTYPE_WEB_HTML** (**0x32**)<br /><br /> **MD_PROPTYPE_WEB_XML_OR_XSL** (**0x33**)<br /><br /> **MD_PROPTYPE_WEB_MAIL_ALIAS** (**0x34**)<br /><br /> **MD_PROPTYPE_ADDRESS** (**되었습니다**)<br /><br /> **MD_PROPTYPE_ADDRESS_STREET** (**0x42**)<br /><br /> **MD_PROPTYPE_ADDRESS_HOUSE** (**0x43**)<br /><br /> **MD_PROPTYPE_ADDRESS_CITY** (**0x44**)<br /><br /> **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (**0x45**)<br /><br /> **MD_PROPTYPE_ADDRESS_ZIP** (**0 x**)<br /><br /> **MD_PROPTYPE_ADDRESS_QUARTER** (**0x47**)<br /><br /> **MD_PROPTYPE_ADDRESS_COUNTRY** (**0x48**)<br /><br /> **MD_PROPTYPE_ADDRESS_BUILDING** (**0x49**)<br /><br /> **MD_PROPTYPE_ADDRESS_ROOM** (**0x4A**)<br /><br /> **MD_PROPTYPE_ADDRESS_FLOOR** (**0x4B**)<br /><br /> **MD_PROPTYPE_ADDRESS_FAX** (**0x4C**)<br /><br /> **MD_PROPTYPE_ADDRESS_PHONE** (**0x4D**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_X** (**0x61**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Y** (**0x62**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Z** (**0x63**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_TOP** (**0x64**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (**0x65**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (**0x66**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (**0x67**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (**0x68**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_REAR** (**0x69**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (**0x6A**)<br /><br /> **MD_PROPTYPE_PHYSICAL_SIZE** (**0x71**)<br /><br /> **MD_PROPTYPE_PHYSICAL_COLOR** (**0x72**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WEIGHT** (**0x73**)<br /><br /> **MD_PROPTYPE_PHYSICAL_HEIGHT** (**0x74**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WIDTH** (**0x75**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DEPTH** (**0x76**)<br /><br /> **MD_PROPTYPE_PHYSICAL_VOLUME** (**0x77**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DENSITY** (**0x78**)<br /><br /> **MD_PROPTYPE_PERSON_FULL_NAME** (**0x82**)<br /><br /> **MD_PROPTYPE_PERSON_FIRST_NAME** (**0x83**)<br /><br /> **MD_PROPTYPE_PERSON_LAST_NAME** (**0x84**)<br /><br /> **MD_PROPTYPE_PERSON_MIDDLE_NAME** (**0x85**)<br /><br /> **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (**0x87**)<br /><br /> **MD_PROPTYPE_PERSON_CONTACT** (**0x87**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_LOW** (**0x91**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_HIGH** (**0x92**)<br /><br /> **MD_PROPTYPE_FORMATTING_COLOR** (**0xA1**)<br /><br /> **MD_PROPTYPE_FORMATTING_ORDER** (**0xA2**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT** (**0xA3**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (**0xA4**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_SIZE** (**0xA5**)<br /><br /> **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (**0xA6**)<br /><br /> **MD_PROPTYPE_DATE** (**0xB1**)<br /><br /> **MD_PROPTYPE_DATE_START** (**0xB2**)<br /><br /> **MD_PROPTYPE_DATE_ENDED** (**0xB3**)<br /><br /> **MD_PROPTYPE_DATE_CANCELED** (**0xB4**)<br /><br /> **MD_PROPTYPE_DATE_MODIFIED** (**0xB5**)<br /><br /> **MD_PROPTYPE_DATE_DURATION** (**0xB6**)<br /><br /> **MD_PROPTYPE_VERSION** (**0xC1**)|  
|**SQL_COLUMN_NAME**|**DBTYPE_WSTR**||큐브 차원 또는 데이터베이스 차원에서 SQL 쿼리에 사용되는 속성의 이름입니다.|  
|**LANGUAGE**|**DBTYPE_UI2**||로 표현 된 번역은 **LCID**합니다. 속성 번역에만 유효합니다.|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**||속성이 적용되는 계층의 유형을 식별합니다.<br /><br /> **MD_USER_DEFINED** (**1**) 사용자 정의 계층에 속성을 나타냅니다<br /><br /> **MD_SYSTEM_ENABLED** (**2**) 속성이 특성 계층에 있음을 나타냅니다<br /><br /> **MD_SYSTEM_DISABLED** (**4**) 속성이 설정 되지 않은 특성 계층에 있음을 나타냅니다.|  
|**PROPERTY_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**||이 속성의 원본을 지정하는 특성 계층의 이름입니다.|  
|**PROPERTY_CARDINALITY**|**DBTYPE_WSTR**||속성의 카디널리티입니다. 가능한 값은 다음 문자열과 같습니다.<br /><br /> **하나**<br /><br /> **많은**|  
|**MIME_TYPE**|**DBTYPE_WSTR**||BLOB(binary large object)의 MIME 형식입니다.|  
|**PROPERTY_IS_VISIBLE**|**DBTYPE_BOOL**||속성이 표시되는지 여부를 나타내는 부울입니다.<br /><br /> **True 이면** 속성이 표시 되 고, 그렇지 않으면 이면 **FALSE**합니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_PROPERTIES** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|필수|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**CUBE_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**PROPERTY_TYPE**|**DBTYPE_I2**|선택 사항|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**|(선택 사항) 에 기본 제한이 적용 됩니다 **MDPROP_MEMBER** 또는 **MDPROP_CELL**합니다.|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**|(선택 사항) 에 기본 제한이 적용 됩니다 **MD_USER_DEFINED** 또는 **MD_SYSTEM_ENABLED**합니다.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다.  유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**PROPERTY_VISIBILITY**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 Visible<br /><br /> 2 Not visible|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP 스키마 행 집합 용 OLE DB](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
