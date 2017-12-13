---
title: "MDSCHEMA_FUNCTIONS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_FUNCTIONS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_FUNCTIONS rowset
ms.assetid: 5253fa8c-b1ce-4504-aff6-a246b5e675c7
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0e25d28e953c3f7a984cf77a4d6d26d34b4f79c0
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="mdschemafunctions-rowset"></a>MDSCHEMA_FUNCTIONS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]데이터베이스에 연결 하는 클라이언트 응용 프로그램에 사용할 수 있는 함수에 설명 합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_FUNCTIONS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|함수의 이름입니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|함수에 대한 설명입니다.|  
|**PARAMETER_LIST**|**DBTYPE_WSTR**|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 형식으로 지정된 쉼표로 구분된 매개 변수 목록입니다. 예를 들어, 매개 변수는 문자열 형식의 이름일 수 있습니다.|  
|**RETURN_TYPE**|**DBTYPE_I4**|**VARTYPE** 함수의 반환 데이터 형식입니다.|  
|**원본**|**DBTYPE_I4**|함수의 기원입니다.<br /><br /> 1 = MDX 함수<br /><br /> 2 = 사용자 정의 함수|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|사용자 정의 함수의 경우 인터페이스 이름입니다.<br /><br /> MDX(Multidimensional Expressions) 함수의 경우 그룹 이름입니다.|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**|사용자 정의 함수의 경우 형식 라이브러리 이름입니다. **NULL** MDX 함수에 대 한 합니다.|  
|**DLL_NAME**|**DBTYPE_WSTR**|(옵션) 사용자 정의 함수를 구현하는 어셈블리 이름입니다.<br /><br /> 반환 **VT_NULL** MDX 함수에 대 한 합니다.|  
|**HELP_FILE**|**DBTYPE_WSTR**|(옵션) 사용자 정의 함수에 대한 도움말 설명서가 있는 파일의 이름입니다.<br /><br /> 반환 **VT_NULL** MDX 함수에 대 한 합니다.|  
|**HELP_CONTEXT**|**DBTYPE_I4**|(옵션) 이 함수에 대한 도움말 컨텍스트 ID를 반환합니다.|  
|**개체**|**DBTYPE_WSTR**|(옵션) 속성이 적용되는 개체 클래스의 일반 이름입니다. 예를 들어 행 집합에 해당 하는 < level_name > 합니다. 멤버 함수에서 반환 "**수준**"입니다.<br /><br /> 반환 **VT_NULL** 사용자 정의 함수 또는 비 속성 MDX 함수에 대 한 합니다.|  
|**캡션**|**DBTYPE_WSTR**|함수의 표시 캡션입니다.|  
  
 에 행 집합은 정렬 **원점**, **INTERFACE_NAME**, **FUNCTION_NAME**합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_FUNCTIONS** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**원본**|**DBTYPE_I4**|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP용 OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
