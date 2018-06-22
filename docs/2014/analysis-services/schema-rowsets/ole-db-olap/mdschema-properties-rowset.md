---
title: MDSCHEMA_PROPERTIES 행 집합 | Microsoft Docs
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
- MDSCHEMA_PROPERTIES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_PROPERTIES rowset
ms.assetid: 95c480f7-c525-44ba-a59b-cd36f5855a4f
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7c0e0506be8f531018285bba9145a587448e743e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082359"
---
# <a name="mdschemaproperties-rowset"></a>MDSCHEMA_PROPERTIES 행 집합
  데이터베이스 내의 멤버 속성을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `MDSCHEMA_PROPERTIES` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||데이터베이스의 이름입니다.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||이 속성이 속한 스키마 이름입니다. 공급자가 스키마를 지원하지 않는 경우 `NULL`입니다.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||큐브의 이름입니다.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||차원의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||계층의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||이 속성이 속한 수준의 고유한 이름입니다. 공급자가 명명된 수준을 지원하지 않는 경우 이 필드에 대해 `DIMENSION_UNIQUE_NAME` 값을 반환해야 합니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`||속성이 속한 멤버의 고유한 이름입니다. 명명된 수준을 지원하지 않거나 멤버별 기준으로 속성을 보유하는 데이터 저장소에 사용됩니다. 속성이 한 수준의 모든 멤버에 적용되면 이 열은 `NULL`입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|`PROPERTY_TYPE`|`DBTYPE_I2`||속성의 유형을 지정하는 비트맵입니다.<br /><br /> -   `MDPROP_MEMBER` (`1`) 멤버의 속성을 식별 합니다. 이 속성은 SELECT 문의 DIMENSION PROPERTIES 절에 사용할 수 있습니다.<br />-   `MDPROP_CELL` (`2`)-셀의 속성을 식별 합니다. 이 속성은 SELECT 문의 끝에 나오는 CELL PROPERTIES 절에 사용할 수 있습니다.<br />-   `MDPROP_SYSTEM` (`4`) 내부 속성을 식별 합니다.<br />-   `MDPROP_BLOB` (`8`) 이진 대형 개체 (blob)을 포함 하는 속성을 식별 합니다.|  
|`PROPERTY_NAME`|`DBTYPE_WSTR`||속성의 이름입니다. 속성의 키가 속성 이름과 같으면 `PROPERTY_NAME`이 비어 있습니다.|  
|`PROPERTY_CAPTION`|`DBTYPE_WSTR`||주로 표시용으로 사용되는, 속성에 연결된 레이블 또는 캡션입니다. 캡션이 없는 경우 `PROPERTY_NAME`을 반환합니다.|  
|`DATA_TYPE`|`DBTYPE_UI2`||속성의 데이터 형식.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||속성이 문자, 이진 또는 비트 유형인 경우 속성에 사용할 수 있는 최대 길이입니다.<br /><br /> 0 값은 정의된 최대 길이가 없음을 나타냅니다.<br /><br /> 그 밖의 다른 데이터 형식의 경우 `NULL`을 반환합니다.|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||속성이 문자 또는 이진 유형인 경우 속성에 사용할 수 있는 최대 길이(바이트)입니다.<br /><br /> 0 값은 정의된 최대 길이가 없음을 나타냅니다.<br /><br /> 그 밖의 다른 데이터 형식의 경우 `NULL`을 반환합니다.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||속성이 숫자 데이터 형식인 경우 속성의 최대 전체 자릿수입니다.<br /><br /> 그 밖의 다른 데이터 형식의 경우 `NULL`을 반환합니다.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||속성이 `DBTYPE_NUMERIC` 또는 `DBTYPE_DECIMAL` 유형인 경우 소수점 오른쪽 자릿수입니다.<br /><br /> 그 밖의 다른 데이터 형식의 경우 `NULL`을 반환합니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||사람이 읽을 수 있는 속성 설명입니다. 설명이 없는 경우 `NULL`입니다.|  
|`PROPERTY_CONTENT_TYPE`|`DBTYPE_I2`||속성의 형식입니다. 다음 열거 중 하나일 수 있습니다.<br /><br /> -   **MD_PROPTYPE_REGULAR** (`0x00`)<br />-   **MD_PROPTYPE_ID** (`0x01`)<br />-   **MD_PROPTYPE_RELATION_TO_PARENT** (`0x02`)<br />-   **MD_PROPTYPE_ROLLUP_OPERATOR** (`0x03`)<br />-   **MD_PROPTYPE_ORG_TITLE** (`0x11`)<br />-   **MD_PROPTYPE_CAPTION** (`0x21`)<br />-   **MD_PROPTYPE_CAPTION_SHORT** (`0x22`)<br />-   **MD_PROPTYPE_CAPTION_DESCRIPTION** (`0x23`)<br />-   **MD_PROPTYPE_CAPTION_ABREVIATION** (`0x24`)<br />-   **MD_PROPTYPE_WEB_URL** (`0x31`)<br />-   **MD_PROPTYPE_WEB_HTML** (`0x32`)<br />-   **MD_PROPTYPE_WEB_XML_OR_XSL** (`0x33`)<br />-   **MD_PROPTYPE_WEB_MAIL_ALIAS** (`0x34`)<br />-   **MD_PROPTYPE_ADDRESS** (`0x41`)<br />-   **MD_PROPTYPE_ADDRESS_STREET** (`0x42`)<br />-   **MD_PROPTYPE_ADDRESS_HOUSE** (`0x43`)<br />-   **MD_PROPTYPE_ADDRESS_CITY** (`0x44`)<br />-   **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (`0x45`)<br />-   **MD_PROPTYPE_ADDRESS_ZIP** (`0x46`)<br />-   **MD_PROPTYPE_ADDRESS_QUARTER** (`0x47`)<br />-   **MD_PROPTYPE_ADDRESS_COUNTRY** (`0x48`)<br />-   **MD_PROPTYPE_ADDRESS_BUILDING** (`0x49`)<br />-   **MD_PROPTYPE_ADDRESS_ROOM** (`0x4A`)<br />-   **MD_PROPTYPE_ADDRESS_FLOOR** (`0x4B`)<br />-   **MD_PROPTYPE_ADDRESS_FAX** (`0x4C`)<br />-   **MD_PROPTYPE_ADDRESS_PHONE** (`0x4D`)<br />-   **MD_PROPTYPE_GEO_CENTROID_X** (`0x61`)<br />-   **MD_PROPTYPE_GEO_CENTROID_Y** (`0x62`)<br />-   **MD_PROPTYPE_GEO_CENTROID_Z** (`0x63`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_TOP** (`0x64`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (`0x65`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (`0x66`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (`0x67`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (`0x68`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_REAR** (`0x69`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (`0x6A`)<br />-   **MD_PROPTYPE_PHYSICAL_SIZE** (`0x71`)<br />-   **MD_PROPTYPE_PHYSICAL_COLOR** (`0x72`)<br />-   **MD_PROPTYPE_PHYSICAL_WEIGHT** (`0x73`)<br />-   **MD_PROPTYPE_PHYSICAL_HEIGHT** (`0x74`)<br />-   **MD_PROPTYPE_PHYSICAL_WIDTH** (`0x75`)<br />-   **MD_PROPTYPE_PHYSICAL_DEPTH** (`0x76`)<br />-   **MD_PROPTYPE_PHYSICAL_VOLUME** (`0x77`)<br />-   **MD_PROPTYPE_PHYSICAL_DENSITY** (`0x78`)<br />-   **MD_PROPTYPE_PERSON_FULL_NAME** (`0x82`)<br />-   **MD_PROPTYPE_PERSON_FIRST_NAME** (`0x83`)<br />-   **MD_PROPTYPE_PERSON_LAST_NAME** (`0x84`)<br />-   **MD_PROPTYPE_PERSON_MIDDLE_NAME** (`0x85`)<br />-   **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (`0x86`)<br />-   **MD_PROPTYPE_PERSON_CONTACT** (`0x87`)<br />-   **MD_PROPTYPE_QTY_RANGE_LOW** (`0x91`)<br />-   **MD_PROPTYPE_QTY_RANGE_HIGH** (`0x92`)<br />-   **MD_PROPTYPE_FORMATTING_COLOR** (`0xA1`)<br />-   **MD_PROPTYPE_FORMATTING_ORDER** (`0xA2`)<br />-   **MD_PROPTYPE_FORMATTING_FONT** (`0xA3`)<br />-   **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (`0xA4`)<br />-   **MD_PROPTYPE_FORMATTING_FONT_SIZE** (`0xA5`)<br />-   **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (`0xA6`)<br />-   **MD_PROPTYPE_DATE** (`0xB1`)<br />-   **MD_PROPTYPE_DATE_START** (`0xB2`)<br />-   **MD_PROPTYPE_DATE_ENDED** (`0xB3`)<br />-   **MD_PROPTYPE_DATE_CANCELED** (`0xB4`)<br />-   **MD_PROPTYPE_DATE_MODIFIED** (`0xB5`)<br />-   **MD_PROPTYPE_DATE_DURATION** (`0xB6`)<br />-   **MD_PROPTYPE_VERSION** (`0xC1`)|  
|`SQL_COLUMN_NAME`|`DBTYPE_WSTR`||큐브 차원 또는 데이터베이스 차원에서 SQL 쿼리에 사용되는 속성의 이름입니다.|  
|`LANGUAGE`|`DBTYPE_UI2`||`LCID`로 표현된 번역입니다. 속성 번역에만 유효합니다.|  
|`PROPERTY_ORIGIN`|`DBTYPE_UI2`||속성이 적용되는 계층의 유형을 식별합니다.<br /><br /> -   `MD_USER_DEFINED` (`1`) 사용자 정의 계층에 속성을 나타냅니다<br />-   `MD_SYSTEM_ENABLED` (`2`) 속성이 특성 계층에 있음을 나타냅니다<br />-   `MD_SYSTEM_DISABLED` (`4`) 속성이 설정 되지 않은 특성 계층에 있음을 나타냅니다.|  
|`PROPERTY_ATTRIBUTE_HIERARCHY_NAME`|`DBTYPE_WSTR`||이 속성의 원본을 지정하는 특성 계층의 이름입니다.|  
|`PROPERTY_CARDINALITY`|`DBTYPE_WSTR`||속성의 카디널리티입니다. 가능한 값은 다음 문자열과 같습니다.<br /><br /> -   `ONE`<br />-   `MANY`|  
|`MIME_TYPE`|`DBTYPE_WSTR`||BLOB(binary large object)의 MIME 형식입니다.|  
|`PROPERTY_IS_VISIBLE`|`DBTYPE_BOOL`||속성이 표시되는지 여부를 나타내는 부울입니다.<br /><br /> 속성이 표시되면 `TRUE`이고, 그렇지 않으면 `FALSE`입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `MDSCHEMA_PROPERTIES` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|필수|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`CUBE_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`PROPERTY_TYPE`|`DBTYPE_I2`|선택 사항|  
|`PROPERTY_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`PROPERTY_CONTENT_TYPE`|`DBTYPE_I2`|(선택 사항) 기본 제한은 `MDPROP_MEMBER` 또는 `MDPROP_CELL`에 적용됩니다.|  
|`PROPERTY_ORIGIN`|`DBTYPE_UI2`|(선택 사항) 기본 제한은 `MD_USER_DEFINED` 또는 `MD_SYSTEM_ENABLED`에 적용됩니다.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|다음 유효 값 중 하나가 포함된 비트맵입니다(선택 사항).<br /><br /> -1 큐브<br />-2 차원<br /><br /> 기본 제한 값은 1입니다.|  
|`PROPERTY_VISIBILITY`|`DBTYPE_UI2`|다음 유효 값 중 하나가 포함된 비트맵입니다(선택 사항).<br /><br /> -1 Visible<br />-2 not 표시<br /><br /> 기본 제한 값은 1입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [OLAP용 OLE DB 스키마 행 집합](ole-db-for-olap-schema-rowsets.md)  
  
  