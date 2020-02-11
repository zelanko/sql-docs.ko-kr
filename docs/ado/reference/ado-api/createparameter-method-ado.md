---
title: CreateParameter 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: af796c36bd2960730536ec07ac49614876311e84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933295"
---
# <a name="createparameter-method-ado"></a>CreateParameter 메서드(ADO)
지정 된 속성을 사용 하 여 새 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>Return Value  
 **매개 변수** 개체를 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 (선택 사항) **매개 변수** 개체의 이름을 포함 하는 **문자열** 값입니다.  
  
 *형식*  
 (선택 사항) **매개 변수** 개체의 데이터 형식을 지정 하는 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 값입니다.  
  
 *방향도*  
 (선택 사항) **매개 변수** 개체의 유형을 지정 하는 [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) 값입니다.  
  
 *크기*  
 (선택 사항) 매개 변수 값의 최대 길이 (문자 또는 바이트)를 지정 하는 **Long** 값입니다.  
  
 *값*  
 (선택 사항) **매개 변수** 개체의 값을 지정 하는 **Variant** 입니다.  
  
## <a name="remarks"></a>설명  
 **Createparameter** 메서드를 사용 하 여 지정 된 이름, 형식, 방향, 크기 및 값을 사용 하 여 새 **매개 변수** 개체를 만듭니다. 인수에서 전달 하는 모든 값은 해당 **매개 변수** 속성에 기록 됩니다.  
  
 이 메서드는 **매개 변수** 개체를 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체의 **Parameters** 컬렉션에 자동으로 추가 하지 않습니다. 이를 통해 컬렉션에 **매개 변수** 개체를 추가할 때 ADO에서 유효성을 검사할 값이 있는 추가 속성을 설정할 수 있습니다.  
  
 *형식* 인수에 가변 길이 데이터 형식을 지정 하는 **경우 매개 변수 컬렉션에** 추가 하기 전에 *크기* 인수를 전달 하거나 **매개 변수** 개체의 [size](../../../ado/reference/ado-api/size-property-ado-parameter.md) 속성을 설정 해야 합니다. 그렇지 않으면 오류가 발생 합니다.  
  
 *형식* 인수에 숫자 데이터 형식 (**Adnumeric** 또는 **adDecimal**)을 지정 하는 경우 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 및 [Precision](../../../ado/reference/ado-api/precision-property-ado.md) 속성도 설정 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Append 및 CreateParameter 메서드 예제 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append 및 CreateParameter 메서드 예제 (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Append 메서드 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)   
 [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
