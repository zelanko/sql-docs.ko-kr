---
title: Source 속성 (ADO 오류) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63407f75c5bee03d24b5b3f69c2ef94cb38e177e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315173"
---
# <a name="source-property-ado-error"></a>Source 속성(ADO 오류)
개체 또는 원래 오류를 생성 한 응용 프로그램의 이름을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **문자열** 개체 또는 응용 프로그램의 이름을 나타내는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **소스** 속성에는 [오류](../../../ado/reference/ado-api/error-object.md) 개체 또는 원래 오류를 생성 한 응용 프로그램의 이름을 확인 하는 개체입니다. 개체의 클래스 이름 또는 프로그래밍 id입니다. Ado에서 오류에 대 한 속성 값이 됩니다 **ADODB.** _ObjectName_, 여기서 *ObjectName* 오류를 트리거한 개체의 이름입니다. ADOX와 ADO MD에 대 한 값이 됩니다 **ADOX.** _ObjectName_ 하 고 **ADOMD.** _ObjectName_, 각각.  
  
 오류 설명서를 기반으로 합니다 **소스**, [번호](../../../ado/reference/ado-api/number-property-ado.md), 및 [설명](../../../ado/reference/ado-api/description-property.md) 의 속성 **오류** 개체 코드를 작성할 수 있습니다 처리 하는 오류를 적절 하 게 합니다.  
  
 합니다 **소스** 에 대 한 읽기 전용 속성은 **오류** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 속성](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext, HelpFile 속성](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 속성 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 속성 (ADO 레코드)](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source 속성(ADO 레코드 집합)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
