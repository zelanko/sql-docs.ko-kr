---
title: MDSCHEMA_SETS 행 집합 | Microsoft Docs
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
- MDSCHEMA_SETS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_SETS rowset
ms.assetid: abb00dc0-2b83-48d6-b2ba-6615c1488d06
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: edc33b87256fb680225eaaa087ff655be1b82851
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186659"
---
# <a name="mdschemasets-rowset"></a>MDSCHEMA_SETS 행 집합
  세션 범위 집합을 비롯하여 데이터베이스에 현재 정의된 집합에 대해 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `MDSCHEMA_SETS` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||데이터베이스의 이름입니다.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||큐브의 이름입니다.|  
|`SET_NAME`|`DBTYPE_WSTR`||`CREATE SET` 문에 지정된 것과 같은 집합 이름입니다.|  
|`SCOPE`|`DBTYPE_I4`||집합의 범위입니다.<br /><br /> -   `MDSET_SCOPE_GLOBAL` (`1`)<br />-   `MDSET_SCOPE_SESSION` (`2`)|  
|`DESCRIPTION`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`EXPRESSION`|`DBTYPE_WSTR`||집합에 대한 식입니다.|  
|`DIMENSIONS`|`DBTYPE_WSTR`||집합에 포함된 계층에 대한 쉼표로 구분된 목록입니다.|  
|`SET_CAPTION`|`DBTYPE_WSTR`||집합에 연결된 레이블 또는 캡션으로 주로 표시 목적으로 사용됩니다.|  
|`SET_DISPLAY_FOLDER`|`DBTYPE_WSTR`||클라이언트 응용 프로그램이 집합을 표시하기 위해 사용하는 표시 폴더의 경로를 식별하는 문자열입니다. 폴더 수준 구분 기호는 클라이언트 응용 프로그램에서 정의합니다. 도구 및에서 제공 하는 클라이언트에 대 한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 백슬래시 (\\)가 수준 구분 기호입니다. 여러 표시 폴더를 제공 하려면 세미콜론 (;)를 사용 하 여 폴더를 구분 합니다.|  
|`SET_EVALUATION_CONTEXT`|`DBTYPE_I4`||집합에 대한 컨텍스트입니다. 집합은 정적이거나 동적일 수 있습니다.<br /><br /> 이 열 값은 다음 중 하나일 수 있습니다.<br /><br /> -MDSET_RESOLUTION_STATIC = 1<br />-MDSET_RESOLUTION_DYNAMIC = 2|  
  
 행 집합은 `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`을 기준으로 정렬됩니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `MDSCHEMA_SETS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`CUBE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`SET_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`SCOPE`|`DBTYPE_I4`|(선택 사항)|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(선택 사항) **참고:** 명명 된 집합만 반환 되는 제한과 정확히 일치 하는 계층 구조 및 계층 하나에 포함 될 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [OLAP용 OLE DB 스키마 행 집합](ole-db-for-olap-schema-rowsets.md)  
  
  