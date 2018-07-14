---
title: DBSCHEMA_COLUMNS 행 집합 | Microsoft Docs
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
- DBSCHEMA_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_COLUMNS rowset
ms.assetid: 653bdd07-a533-4a99-8b6a-6e5c7322e1f3
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6fa933eb153b0d8de4c2fec4ba92b072954be141
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267579"
---
# <a name="dbschemacolumns-rowset"></a>DBSCHEMA_COLUMNS 행 집합
  제공된 제한 조건을 충족하는 모든 열의 열 정보를 제공합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DBSCHEMA_COLUMNS` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`||데이터베이스의 이름입니다.|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`TABLE_NAME`|`DBTYPE_WSTR`||큐브의 이름입니다.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||특성 계층 또는 측정값의 이름입니다.|  
|`COLUMN_GUID`|`DBTYPE_GUID`||지원되지 않습니다.|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||지원되지 않습니다.|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||1부터 시작하는 열 위치입니다.|  
|`COLUMN_HAS_DEFAULT`|`DBTYPE_BOOL`||지원되지 않습니다.|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||열 속성을 나타내는 `DBCOLUMNFLAGS` 비트 마스크입니다. 'DBCOLUMNFLAGS 열거 형식'에 나오는 [icolumnsinfo:: Getcolumninfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||항상 반환 `false`합니다.|  
|`DATA_TYPE`|`DBTYPE_WSTR`<br /><br /> `DBTYPE_VARIANT`||열의 데이터 형식입니다. 차원 열의 경우 문자열을 반환하고 측정값의 경우 변형을 반환합니다.|  
|`TYPE_GUID`|`DBTYPE_GUID`||지원되지 않습니다.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||열 값의 최대 길이입니다.<br /><br /> 이 열은 `DataSize`의 `DataItem` 속성에서 검색됩니다.|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||문자 또는 이진 열의 경우 열 값의 최대 길이(바이트)입니다.<br /><br /> 0 값은 열에 최대 길이가 없음을 나타냅니다.<br /><br /> 이진 또는 문자 데이터 형식을 반환하지 않는 열의 경우 `NULL`이 반환됩니다.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||`DBTYPE_VARNUMERIC`이 아닌 숫자 데이터 형식의 경우 열의 최대 전체 자릿수입니다.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||`DBTYPE_DECIMAL`, `DBTYPE_NUMERIC`, `DBTYPE_VARNUMERIC`의 경우 소수점 이하 자릿수입니다. 그렇지 않으면 `NULL`입니다.|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||지원되지 않습니다.|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`||개체의 OLAP 유형입니다.<br /><br /> `MEASURE`는 개체가 측정값임을 나타냅니다.<br /><br /> `ATTRIBUTE`는 개체가 차원 특성임을 나타냅니다.<br /><br /> `SCHEMA`는 개체가 스키마의 열임을 나타냅니다.|  
  
 행 집합은 `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`을 기준으로 정렬됩니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `DBSCHEMA_COLUMNS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|선택 사항|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|선택 사항|  
|`TABLE_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`|선택 사항|  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB 스키마 행 집합](ole-db-schema-rowsets.md)  
  
  
