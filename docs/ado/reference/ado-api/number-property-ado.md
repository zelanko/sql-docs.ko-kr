---
title: Number 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce027747c843e02998f4845db7075e70cf8733b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917991"
---
# <a name="number-property-ado"></a>Number 속성(ADO)
[오류](../../../ado/reference/ado-api/error-object.md) 개체를 고유 하 게 식별 하는 번호를 나타냅니다.  
  
## <a name="return-value"></a>Return Value  
 [Errorvalueenum](../../../ado/reference/ado-api/errorvalueenum.md) 상수 중 하나에 해당할 수 있는 **Long** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Number** 속성을 사용 하 여 발생 한 오류를 확인 합니다. 속성의 값은 오류 조건에 해당 하는 고유 번호입니다.  
  
 [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션은 16 진수 형식 (예: 0x80004005) 또는 long 값 (예: 2147467259)의 HRESULT를 반환 합니다. 이러한 Hresult는 OLE DB 또는 OLE 자체와 같은 기본 구성 요소에 의해 발생할 수 있습니다. 이러한 숫자에 대 한 자세한 내용은 [OLE DB 프로그래머 참조](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)에서 [오류 (OLE DB)](https://msdn.microsoft.com/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd) 를 참조*하세요.*  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 속성](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext, HelpFile 속성](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Source 속성(ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)
