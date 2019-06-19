---
title: HelpContext, HelpFile 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c9c980e293b06e7fa9642ace7d425b7ffd3c0197
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694809"
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext, HelpFile 속성
도움말 파일 및 연결 된 항목을 나타냅니다는 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다.  
  
## <a name="return-values"></a>반환 값  
  
-   **HelpContextID** 컨텍스트 ID를 반환 된 **긴** 도움말 파일의 항목에 대 한 값.  
  
-   **HelpFile** 반환 된 **문자열** 도움말 파일의 전체 경로가으로 계산 되는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 도움말 파일에 지정 된 경우는 **HelpFile** 속성을 **HelpContext** 속성 자동으로 식별 하는 도움말 항목을 표시 하는 데 사용 됩니다. 를 사용할 수 있는 관련 도움말 항목이 없으면를 **HelpContext** 0을 반환 하는 속성 및 **HelpFile** 길이가 0 인 문자열을 반환 하는 속성 ("").  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 속성](../../../ado/reference/ado-api/description-property.md)   
 [Number 속성 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 속성(ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)
