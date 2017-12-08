---
title: "MDSCHEMA_ACTIONS 행 집합 | Microsoft Docs"
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
apiname: MDSCHEMA_ACTIONS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_ACTIONS rowset
ms.assetid: f73081f8-ac51-4286-b46e-2b34e792c3e0
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b2957bca5aee8c0894e7139c46beab26fe2c74f0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemaactions-rowset"></a>MDSCHEMA_ACTIONS 행 집합
  클라이언트 응용 프로그램에 사용할 수 있는 동작을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_ACTIONS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||데이터베이스의 이름입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||지원되지 않습니다. 항상 포함 **VT_NULL**합니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||이 동작이 속한 큐브의 이름입니다.|  
|**ACTION_NAME**|**DBTYPE_WSTR**||이 동작의 이름입니다.|  
|**ACTION_TYPE**|**DBTYPE_I4**||동작의 트리거 방법을 지정하는 데 사용되는 비트맵입니다. 이 비트맵에 대해 다음 비트 값 상수가 Msmd.h 파일에 정의됩니다.<br /><br /> **MDACTION_TYPE_URL** (**0x01**)<br /><br /> **MDACTION_TYPE_HTML** (**0x02**)<br /><br /> **MDACTION_TYPE_STATEMENT** (**0x04**)<br /><br /> **MDACTION_TYPE_DATASET** (**0x08**)<br /><br /> **MDACTION_TYPE_ROWSET** (**0x10**)<br /><br /> **MDACTION_TYPE_COMMANDLINE** (**0x20**)<br /><br /> **MDACTION_TYPE_PROPRIETARY** (**0x40**)<br /><br /> **MDACTION_TYPE_REPORT** (**0x80**)<br /><br /> **MDACTION_TYPE_DRILLTHROUGH** (**0x100**)|  
|**좌표**|**DBTYPE_WSTR**||동작이 수행되는 다차원 공간에서 개체 또는 좌표를 지정하는 MDX(Multidimensional Expressions) 식입니다. 이 제한 열의 값을 제공하는 것은 클라이언트 응용 프로그램에서 담당합니다.<br /><br /> **CORDINATE** 에 지정 된 개체를 확인 해야 **COORDINATE_TYPE**합니다.|  
|**COORDINATE_TYPE**|**DBTYPE_I4**||지정 하는 비트맵 방법을 **조정** 제한 열은 해석 됩니다. 이 비트맵에 대해 다음 비트 값 상수가 Msmd.h 파일에 정의됩니다.<br /><br /> **MDACTION_COORDINATE_CUBE** (**1**)<br /><br /> **MDACTION_COORDINATE_DIMENSION** (**2**): 차원 계층을 가리킵니다.<br /><br /> **MDACTION_COORDINATE_LEVEL** (**3**)<br /><br /> **MDACTION_COORDINATE_MEMBER** (**4**)<br /><br /> **MDACTION_COORDINATE_SET** (**5**)<br /><br /> **MDACTION_COORDINATE_CELL** (**6**)|  
|**ACTION_CAPTION**|**DBTYPE_WSTR**||DDL에 지정된 캡션과 지정된 번역이 없는 경우 동작 이름입니다.<br /><br /> 캡션 또는 번역이 지정 된 경우 및 **CaptionIsMDX** 이 false 이면 다음 문자열 중 하나:<br /><br /> -적절 한 언어에 대 한 변환입니다.<br /><br /> 지정된 된 언어에 대 한 변환을 찾을 수 없으면-지정 된 캡션<br /><br /> 변환을 찾을 수 없으면-작업 이름 및 캡션에 DDL에 지정 되지 않았습니다.<br /><br /> 캡션 또는 번역이 지정 된 경우 및 **CaptionIsMDX** 가 true 이면 지정된 된 언어 또는 DDL 캡션의 지정 된 번역에 대 한 적절 한 번역을 찾아서 계산 결과 문자열이 고 문자열을 만드는 수식입니다.<br /><br /> MDX 스크립트에 동작이 지정된 경우 번역이 없고 캡션은 항상 MDX 식으로 처리됩니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||동작에 대한 알기 쉬운 설명입니다.|  
|**콘텐츠**|**DBTYPE_WSTR**||실행할 동작의 식 또는 내용입니다.|  
|**응용 프로그램**|**DBTYPE_WSTR**||동작을 실행하는 데 사용할 응용 프로그램의 이름입니다.|  
|**호출**|**DBTYPE_I4**||동작이 호출되는 방법에 대한 정보입니다.<br /><br /> **MDACTION_INVOCATION_INTERACTIVE** (**1**) 정상 작업 중 사용 되는 일반 동작을 나타냅니다. 이 열의 기본값입니다.<br /><br /> **MDACTION_INVOCATION_ON_OPEN** (**2**) 큐브가 처음 열릴 때 동작을 수행 해야 함을 나타냅니다.<br /><br /> **MDACTION_INVOCATION_BATCH** (**4**) 작업 일괄 처리 작업의 일환으로 수행 됨을 나타냅니다 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 작업 합니다.<br /><br /> <br /><br /> 이 열거형 값 Msmd.h 파일에 정의 되어 있는지 확인 합니다.|  
  
 에 행 집합은 정렬 **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **ACTION_NAME**합니다.  
  
> [!NOTE]  
>  작업의 **MDACTION_TYPE_PROPRIETARY** 형식에 대 한 값을 제공 해야 합니다는 **응용 프로그램** 열입니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_ACTIONS** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**CUBE_NAME**|**DBTYPE_WSTR**|필수|  
|**ACTION_NAME**|**DBTYPE_WSTR**|선택 사항|  
|**ACTION_TYPE**|**DBTYPE_I4**|선택 사항|  
|**좌표**|**DBTYPE_WSTR**|필수|  
|**COORDINATE_TYPE**|**DBTYPE_I4**|필수|  
|**호출**|**DBTYPE_I4**|(선택 사항) **호출** 제한 열의 값을 기본값 **MDACTION_INVOCATION_INTERACTIVE**합니다. 모든 작업을 검색 하려면는 **MDACTION_INVOCATION_ALL** 값에 **호출** 제한 열입니다.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
  
> [!IMPORTANT]  
>  **호출** 제한 열에는 기본값인 **MDACTION_INVOCATION_INTERACTIVE**합니다. 이 열에 명시적으로 값을 지정하지 않은 스키마 행 집합은 이 값을 가진 행만 포함합니다. 사용 하 여 행 집합에 전체 동작 집합이 포함 하려는 경우는 **MDACTION_INVOCATION_ALL** 에 상수는 **호출** 제한 열입니다.  
  
 클라이언트 응용 프로그램이 여러 개 정의할 수 **ACTION_TYPE** OR 연산자를 사용 하 여 합니다.  
  
## <a name="remarks"></a>주의  
 다음 표에서 유효한 **조정** 및 **COORDINATE_TYPE** 조합 합니다.  
  
|COORDINATE 개체 유형|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|**Cube**|**MDACTION_COORDINATE_CUBE**|  
|**Dimension**|**MDACTION_COORDINATE_DIMENSION**<br /><br /> **MDACTION_COORDINATE_LEVEL**<br /><br /> **MDACTION_COORDINATE_MEMBER**<br /><br /> **MDACTION_COORDINATE_SET**<br /><br /> **MDACTION_COORDINATE_CELL**|  
|**Hierarchy**|**MDACTION_COORDINATE_DIMENSION**|  
|**Level**|**MDACTION_COORDINATE_LEVEL**|  
|**멤버**|**MDACTION_COORDINATE_MEMBER**|  
|**설정**|**MDACTION_COORDINATE_SET**|  
|**셀**|**MDACTION_COORDINATE_CELL**|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP용 OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
