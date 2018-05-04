---
title: Number 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 592390f1ae5fd6e1e8087d7c33062e2b271af3eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="number-property-ado"></a>Number 속성 (ADO)
고유 하 게 식별 하는 번호 나타냅니다는 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **긴** 값 중 하나에 해당 하는 [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) 상수입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **번호** 발생 한 오류를 확인 하는 속성입니다. 속성의 값은 오류 조건에 해당 하는 고유한 번호입니다.  
  
 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션 16 진수 형식 (예를 들어 0x80004005) 또는 long 값 (예를 들어 2147467259) HRESULT를 반환 합니다. 이러한 Hresult와 같은 OLE DB 또는 자체에 OLE 내부 구성 요소에 의해 발생할 수 있습니다. 이러한 번호에 대 한 자세한 내용은 참조 [오류 (OLE DB)](http://msdn.microsoft.com/en-us/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd) 에 [OLE DB Programmer's Reference](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)*합니다.*  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 속성](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext, 도움말 파일 속성](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Source 속성(ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)
