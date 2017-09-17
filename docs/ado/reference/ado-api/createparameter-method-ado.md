---
title: "CreateParameter 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a7fc09313bffacefd2d9eff86c9176222c094ebe
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="createparameter-method-ado"></a>CreateParameter 메서드 (ADO)
새 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체 속성을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **매개 변수** 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 (선택 사항) A **문자열** 값의 이름을 포함 하는 **매개 변수** 개체입니다.  
  
 *형식*  
 (선택 사항) A [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 값의 데이터 형식을 지정 하는 **매개 변수** 개체입니다.  
  
 *방향*  
 (선택 사항) A [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) 의 유형을 지정 하는 값 **매개 변수** 개체입니다.  
  
 *크기*  
 (선택 사항) A **긴** 문자 또는 바이트에서 매개 변수 값에 대 한 최대 길이 지정 하는 값입니다.  
  
 *Value*  
 (선택 사항) A **Variant** 에 대 한 값을 지정 하는 **매개 변수** 개체입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **CreateParameter** 만드는 새 메서드를 **매개 변수** 지정 된 이름, 유형, 방향, 크기 및 값 개체입니다. 인수에 전달 된 값에 해당 요소에 기록 됩니다 **매개 변수** 속성입니다.  
  
 이 메서드는 자동으로 추가 하지 않습니다는 **매개 변수** 개체는 **매개 변수** 의 컬렉션은 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다. 이렇게 하면 추가 하는 경우 ADO에서 해당 값은 유효성을 검사 하는 추가 속성을 설정할 수 있습니다는 **매개 변수** 개체 컬렉션입니다.  
  
 가변 길이 데이터 형식에 지정 하는 경우는 *형식* 인수 중 하나를 전달 해야 합니다는 *크기* 인수 또는 설정은 [크기](../../../ado/reference/ado-api/size-property-ado-parameter.md) 의 속성은 **매개 변수 ** 개체에 추가 하기 전에 **매개 변수** 컬렉션, 그렇지 않으면 오류가 발생 합니다.  
  
 숫자 데이터 형식을 지정 하면 (**adNumeric** 또는 **adDecimal**)에 *형식* 다음 인수를 설정 해야는 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 및 [정밀도](../../../ado/reference/ado-api/precision-property-ado.md) 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [추가 및 CreateParameter 메서드 예제 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [추가 및 CreateParameter 메서드 예제 (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Append 메서드 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)   
 [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)

