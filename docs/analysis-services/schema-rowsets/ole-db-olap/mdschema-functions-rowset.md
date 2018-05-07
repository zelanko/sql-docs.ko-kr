---
title: MDSCHEMA_FUNCTIONS 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81c5ff06837dd9004be1ffc72be017a4991e902f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemafunctions-rowset"></a>MDSCHEMA_FUNCTIONS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  데이터베이스에 연결된 클라이언트 응용 프로그램에 사용할 수 있는 함수를 설명합니다.  
  
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
|**OBJECT**|**DBTYPE_WSTR**|(옵션) 속성이 적용되는 개체 클래스의 일반 이름입니다. 예를 들어 행 집합에 해당 하는 < level_name > 합니다. 멤버 함수에서 반환 "**수준**"입니다.<br /><br /> 반환 **VT_NULL** 사용자 정의 함수 또는 비 속성 MDX 함수에 대 한 합니다.|  
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
 [OLAP 스키마 행 집합 용 OLE DB](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
