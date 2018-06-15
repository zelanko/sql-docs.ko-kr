---
title: MDSCHEMA_SETS 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 666f8aa8889f2d15e9e62499e41ad9c0bc69fcff
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34028054"
---
# <a name="mdschemasets-rowset"></a>MDSCHEMA_SETS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  세션 범위 집합을 비롯하여 데이터베이스에 현재 정의된 집합에 대해 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_SETS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|데이터베이스의 이름입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|지원되지 않습니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|큐브의 이름입니다.|  
|**SET_NAME**|**DBTYPE_WSTR**|에 지정 된 집합의 이름을 **CREATE SET** 문.|  
|**범위**|**DBTYPE_I4**|집합의 범위입니다.<br /><br /> **MDSET_SCOPE_GLOBAL** (**1**)<br /><br /> **MDSET_SCOPE_SESSION** (**2**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|지원되지 않습니다.|  
|**식**|**DBTYPE_WSTR**|집합에 대한 식입니다.|  
|**차원**|**DBTYPE_WSTR**|집합에 포함된 계층에 대한 쉼표로 구분된 목록입니다.|  
|**SET_CAPTION**|**DBTYPE_WSTR**|집합에 연결된 레이블 또는 캡션으로 주로 표시 목적으로 사용됩니다.|  
|**SET_DISPLAY_FOLDER**|**DBTYPE_WSTR**|클라이언트 응용 프로그램이 집합을 표시하기 위해 사용하는 표시 폴더의 경로를 식별하는 문자열입니다. 폴더 수준 구분 기호는 클라이언트 응용 프로그램에서 정의합니다. 도구 및에서 제공 하는 클라이언트에 대 한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 백슬래시 (\\)가 수준 구분 기호입니다. 여러 표시 폴더를 제공 하려면 세미콜론 (;)를 사용 하 여 폴더를 구분 합니다.|  
|**SET_EVALUATION_CONTEXT**|**DBTYPE_I4**|집합에 대한 컨텍스트입니다. 집합은 정적이거나 동적일 수 있습니다. 이 열 값은 다음 중 하나일 수 있습니다.<br /><br /> MDSET_RESOLUTION_STATIC=1<br /><br /> MDSET_RESOLUTION_DYNAMIC=2|  
  
 행 집합은 **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**을 기준으로 정렬됩니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_SETS** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SET_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**범위**|**DBTYPE_I4**|(선택 사항)|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항)<br /><br /> 참고: 계층 하나에 포함 될 수 및 명명 된 집합만 반환 되는 계층이 제한을 정확 하 게 일치 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP 스키마 행 집합 용 OLE DB](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
