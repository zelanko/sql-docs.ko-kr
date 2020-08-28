---
description: HelpContext, HelpFile 속성
title: HelpContext, HelpFile 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d9ac9c7f712514f50ab8d40704700924ac344d23
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990844"
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext, HelpFile 속성
[오류](./error-object.md) 개체와 연결 된 도움말 파일 및 항목을 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
  
-   **HelpContextID** 도움말 파일의 항목에 대 한 컨텍스트 ID를 **Long** 값으로 반환 합니다.  
  
-   **HelpFile** 도움말 파일에 대 한 완전히 확인 된 경로로 계산 되는 **문자열** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 도움말 파일이 **HelpFile** 속성에 지정 된 경우 **HelpContext** 속성을 사용 하 여 식별 되는 도움말 항목을 자동으로 표시 합니다. 사용할 수 있는 관련 도움말 항목이 없으면 **HelpContext** 속성은 0을 반환 하 고 **HelpFile** 속성은 길이가 0 인 문자열 ("")을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](./error-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 속성](./description-property.md)   
 [Number 속성 (ADO)](./number-property-ado.md)   
 [Source 속성(ADO 오류)](./source-property-ado-error.md)