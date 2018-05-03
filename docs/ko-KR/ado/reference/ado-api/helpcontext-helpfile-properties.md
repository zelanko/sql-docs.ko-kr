---
title: HelpContext, HelpFile 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetHelpContext
- Error::GetHelpFile
- Error::get_HelpFile
- Error::get_HelpContext
- Error::HelpContext
- Error::HelpFile
helpviewer_keywords:
- HelpContext property [ADO]
- HelpFile property [ADO]
ms.assetid: 2b9ef441-993c-44d4-8f87-fac0979dac1d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74b6cab9fdd337bef8b36da027abbd7d7d87bb57
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext, 도움말 파일 속성
도움말 파일 및 관련 된 항목을 나타냅니다는 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다.  
  
## <a name="return-values"></a>반환 값  
  
-   **HelpContextID** 로 컨텍스트 ID를 반환는 **긴** 도움말 파일의 항목에 대 한 값입니다.  
  
-   **HelpFile** 반환은 **문자열** 는 도움말 파일의 전체 경로가으로 계산 되는 값입니다.  
  
## <a name="remarks"></a>주의  
 도움말 파일을 지정 하는 경우는 **HelpFile** 속성에는 **HelpContext** 속성은 자동으로 식별 하는 도움말 항목을 표시 하는 데 사용 합니다. 를 사용할 수 없는 관련 도움말 항목 경우는 **HelpContext** 0을 반환 하는 속성 및 **HelpFile** 길이가 0 인 문자열을 반환 하는 속성 ("").  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 속성](../../../ado/reference/ado-api/description-property.md)   
 [Number 속성 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 속성(ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)
