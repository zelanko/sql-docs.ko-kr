---
title: MDSCHEMA_FUNCTIONS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_FUNCTIONS rowset
ms.assetid: 5253fa8c-b1ce-4504-aff6-a246b5e675c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d5966a975cab0f70c24801e83ee9eab7fa99398
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090873"
---
# <a name="mdschemafunctions-rowset"></a>MDSCHEMA_FUNCTIONS 행 집합
  데이터베이스에 연결된 클라이언트 응용 프로그램에 사용할 수 있는 함수를 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 합니다 **MDSCHEMA_FUNCTIONS** 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**||함수의 이름입니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||함수에 대한 설명입니다.|  
|**PARAMETER_LIST**|**DBTYPE_WSTR**||[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 형식으로 지정된 쉼표로 구분된 매개 변수 목록입니다. 예를 들어, 매개 변수는 문자열 형식의 이름일 수 있습니다.|  
|**RETURN_TYPE**|**DBTYPE_I4**||합니다 **VARTYPE** 함수의 반환 데이터 형식입니다.|  
|**원본**|**DBTYPE_I4**||함수의 기원입니다.<br /><br /> -1 = MDX 함수입니다.<br />사용자 정의 함수에 대 한 2입니다.|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**||사용자 정의 함수의 경우 인터페이스 이름입니다.<br /><br /> MDX(Multidimensional Expressions) 함수의 경우 그룹 이름입니다.|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**||사용자 정의 함수의 경우 형식 라이브러리 이름입니다. **NULL** MDX 함수에 대 한 합니다.|  
|**DLL_NAME**|**DBTYPE_WSTR**||(옵션) 사용자 정의 함수를 구현하는 어셈블리 이름입니다.<br /><br /> 반환 **VT_NULL** MDX 함수에 대 한 합니다.|  
|**HELP_FILE**|**DBTYPE_WSTR**||(옵션) 사용자 정의 함수에 대한 도움말 설명서가 있는 파일의 이름입니다.<br /><br /> 반환 **VT_NULL** MDX 함수에 대 한 합니다.|  
|**HELP_CONTEXT**|**DBTYPE_I4**||(옵션) 이 함수에 대한 도움말 컨텍스트 ID를 반환합니다.|  
|**OBJECT**|**DBTYPE_WSTR**||(옵션) 속성이 적용되는 개체 클래스의 일반 이름입니다. 예를 들어, 행 집합 < level_name >에 해당 합니다. 멤버 함수에서 반환 "**수준**"입니다.<br /><br /> 반환 **VT_NULL** 사용자 정의 함수 또는 비 속성 MDX 함수에 대 한 합니다.|  
|**캡션**|**DBTYPE_WSTR**||함수의 표시 캡션입니다.|  
  
 행 집합을 기준으로 정렬 됩니다 **원본**를 **INTERFACE_NAME**하십시오 **FUNCTION_NAME**합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 합니다 **MDSCHEMA_FUNCTIONS** 다음 표에 나열 된 열에서 행 집합을 제한할 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**원본**|**DBTYPE_I4**|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [OLAP용 OLE DB 스키마 행 집합](ole-db-for-olap-schema-rowsets.md)  
  
  
