---
title: "Source 속성 (ADO 오류) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords: Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a0f34bfbe5c4d7fa251316658dd76878c7b53c5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="source-property-ado-error"></a>Source 속성 (ADO 오류)
개체 또는 원래 오류를 생성 한 응용 프로그램의 이름을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **문자열** 개체 또는 응용 프로그램의 이름을 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **소스** 속성에는 [오류](../../../ado/reference/ado-api/error-object.md) 개체 또는 원래 오류를 생성 한 응용 프로그램의 이름을 결정 하는 개체입니다. 개체의 클래스 이름 또는 프로그래밍 id입니다.가 수 있습니다. Ado에서 오류에 대 한 속성 값이 됩니다 **ADODB.** *ObjectName*여기서 *ObjectName* 오류를 발생 시킨 개체의 이름입니다. ADOX 및 ADO MD에 대 한 값은 됩니다 **ADOX.** *ObjectName* 및 **ADOMD.** *ObjectName* 각각.  
  
 오류 설명서에 따라는 **소스**, [번호](../../../ado/reference/ado-api/number-property-ado.md), 및 [설명](../../../ado/reference/ado-api/description-property.md) 의 속성 **오류** 개체 코드를 작성할 수 있습니다 오류를 적절 하 게 처리 합니다입니다.  
  
 **소스** 에 대 한 읽기 전용 속성은 **오류** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 속성](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext, 도움말 파일 속성](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 속성 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 속성 (ADO 레코드)](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source 속성(ADO 레코드 집합)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
