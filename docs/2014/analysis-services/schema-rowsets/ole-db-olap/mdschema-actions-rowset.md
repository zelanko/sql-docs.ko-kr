---
title: MDSCHEMA_ACTIONS 행 집합 | Microsoft Docs
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
- MDSCHEMA_ACTIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_ACTIONS rowset
ms.assetid: f73081f8-ac51-4286-b46e-2b34e792c3e0
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7382056922a52e734df61015df85930682d0db0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319373"
---
# <a name="mdschemaactions-rowset"></a>MDSCHEMA_ACTIONS 행 집합
  클라이언트 응용 프로그램에 사용할 수 있는 동작을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `MDSCHEMA_ACTIONS` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||데이터베이스의 이름입니다.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||지원되지 않습니다. 항상 `VT_NULL`을 포함합니다.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||이 동작이 속한 큐브의 이름입니다.|  
|`ACTION_NAME`|`DBTYPE_WSTR`||이 동작의 이름입니다.|  
|`ACTION_TYPE`|`DBTYPE_I4`||동작의 트리거 방법을 지정하는 데 사용되는 비트맵입니다. 이 비트맵에 대해 다음 비트 값 상수가 Msmd.h 파일에 정의됩니다.<br /><br /> -   `MDACTION_TYPE_URL` (`0x01`)<br />-   `MDACTION_TYPE_HTML` (`0x02`)<br />-   `MDACTION_TYPE_STATEMENT` (`0x04`)<br />-   `MDACTION_TYPE_DATASET` (`0x08`)<br />-   `MDACTION_TYPE_ROWSET` (`0x10`)<br />-   `MDACTION_TYPE_COMMANDLINE` (`0x20`)<br />-   `MDACTION_TYPE_PROPRIETARY` (`0x40`)<br />-   `MDACTION_TYPE_REPORT` (`0x80`)<br />-   `MDACTION_TYPE_DRILLTHROUGH` (`0x100`)|  
|`COORDINATE`|`DBTYPE_WSTR`||동작이 수행되는 다차원 공간에서 개체 또는 좌표를 지정하는 MDX(Multidimensional Expressions) 식입니다. 이 제한 열의 값을 제공하는 것은 클라이언트 응용 프로그램에서 담당합니다.<br /><br /> `CORDINATE`에서 `COORDINATE_TYPE`에 지정된 개체를 분석해야 합니다.|  
|`COORDINATE_TYPE`|`DBTYPE_I4`||`COORDINATE` 제한 열이 해석되는 방법을 지정하는 비트맵입니다. 이 비트맵에 대해 다음 비트 값 상수가 Msmd.h 파일에 정의됩니다.<br /><br /> -   `MDACTION_COORDINATE_CUBE` (`1`)<br />-   `MDACTION_COORDINATE_DIMENSION` (`2`)<br />     차원 계층을 참조합니다.<br />-   `MDACTION_COORDINATE_LEVEL` (`3`)<br />-   `MDACTION_COORDINATE_MEMBER` (`4`)<br />-   `MDACTION_COORDINATE_SET` (`5`)<br />-   `MDACTION_COORDINATE_CELL` (`6`)|  
|`ACTION_CAPTION`|`DBTYPE_WSTR`||DDL에 지정된 캡션과 지정된 번역이 없는 경우 동작 이름입니다.<br /><br /> 캡션 또는 번역이 지정되었고 `CaptionIsMDX`가 False인 경우 다음 문자열 중 하나입니다.<br /><br /> -해당 언어에 대 한 변환입니다.<br />-지정 된 캡션 변환이 없는 지정된 된 언어에 대 한 검색 된 경우.<br />찾을 수 없는 변환 하는 경우-작업 이름 및 캡션에 DDL에 지정 되지 않았습니다.<br /><br /> 캡션 또는 번역이 지정되었고 `CaptionIsMDX`가 True인 경우 지정된 언어에 해당하는 번역 또는 DDL 캡션의 지정된 번역을 찾아서 문자열을 만드는 수식을 계산하면 결과 문자열이 나옵니다.<br /><br /> MDX 스크립트에 동작이 지정된 경우 번역이 없고 캡션은 항상 MDX 식으로 처리됩니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||동작에 대한 알기 쉬운 설명입니다.|  
|`CONTENT`|`DBTYPE_WSTR`||실행할 동작의 식 또는 내용입니다.|  
|`APPLICATION`|`DBTYPE_WSTR`||동작을 실행하는 데 사용할 응용 프로그램의 이름입니다.|  
|`INVOCATION`|`DBTYPE_I4`||동작이 호출되는 방법에 대한 정보입니다.<br /><br /> -   `MDACTION_INVOCATION_INTERACTIVE` (`1`) 정상 작업 중 사용 되는 일반 동작을 나타냅니다. 이 열의 기본값입니다.<br />-   `MDACTION_INVOCATION_ON_OPEN` (`2`) 큐브를 처음 열 때 작업을 수행할 수를 나타냅니다.<br />-   `MDACTION_INVOCATION_BATCH` (`4`) 작업을 일괄 처리 작업의 일환으로 수행 됨을 나타냅니다 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 작업 합니다.<br /><br /> 이러한 열거 값은 Msmd.h 파일에 정의됩니다.|  
  
 행 집합은 `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `ACTION_NAME`을 기준으로 정렬됩니다.  
  
> [!NOTE]  
>  `MDACTION_TYPE_PROPRIETARY` 유형의 동작은 `APPLICATION` 열에 값을 제공해야 합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `MDSCHEMA_ACTIONS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`CUBE_NAME`|`DBTYPE_WSTR`|필수|  
|`ACTION_NAME`|`DBTYPE_WSTR`|선택 사항|  
|`ACTION_TYPE`|`DBTYPE_I4`|선택 사항|  
|`COORDINATE`|`DBTYPE_WSTR`|필수|  
|`COORDINATE_TYPE`|`DBTYPE_I4`|필수|  
|`INVOCATION`|`DBTYPE_I4`|(옵션) `INVOCATION` 제한 열의 기본값은 `MDACTION_INVOCATION_INTERACTIVE`입니다. 모든 동작을 검색하려면 `MDACTION_INVOCATION_ALL` 제한 열에서 `INVOCATION` 값을 사용하십시오.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|다음 유효 값 중 하나가 포함된 비트맵입니다(선택 사항).<br /><br /> -1 큐브<br />-2 차원<br /><br /> 기본 제한 값은 1입니다.|  
  
> [!IMPORTANT]  
>  `INVOCATION` 제한 열의 기본값은 `MDACTION_INVOCATION_INTERACTIVE`입니다. 이 열에 명시적으로 값을 지정하지 않은 스키마 행 집합은 이 값을 가진 행만 포함합니다. 행 집합에 전체 동작 집합이 포함되도록 하려면 `MDACTION_INVOCATION_ALL` 제한 열에서 `INVOCATION` 상수를 사용하십시오.  
  
 클라이언트 응용 프로그램은 OR 연산자를 사용하여 여러 개의 `ACTION_TYPE`을 정의할 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 다음 표에서는 유효한 `COORDINATE` 및 `COORDINATE_TYPE` 조합을 나열합니다.  
  
|COORDINATE 개체 유형|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|`Cube`|`MDACTION_COORDINATE_CUBE`|  
|`Dimension`|`MDACTION_COORDINATE_DIMENSION`<br /><br /> `MDACTION_COORDINATE_LEVEL`<br /><br /> `MDACTION_COORDINATE_MEMBER`<br /><br /> `MDACTION_COORDINATE_SET`<br /><br /> `MDACTION_COORDINATE_CELL`|  
|`Hierarchy`|`MDACTION_COORDINATE_DIMENSION`|  
|`Level`|`MDACTION_COORDINATE_LEVEL`|  
|`Member`|`MDACTION_COORDINATE_MEMBER`|  
|`Set`|`MDACTION_COORDINATE_SET`|  
|`cell`|`MDACTION_COORDINATE_CELL`|  
  
## <a name="see-also"></a>관련 항목  
 [OLAP용 OLE DB 스키마 행 집합](ole-db-for-olap-schema-rowsets.md)  
  
  
