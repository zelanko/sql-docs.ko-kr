---
title: Size 속성 (ADO 매개 변수) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3796f772dedb961ec34eb0639034350989f99142
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931050"
---
# <a name="size-property-ado-parameter"></a>Size 속성(ADO 매개 변수)
[매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체의 최대 크기 (바이트 또는 문자)를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **매개 변수** 개체에 있는 값의 최대 크기 (바이트 또는 문자)를 나타내는 **Long** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Size** 속성을 사용 하 여 **매개 변수** 개체의 [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성에 쓰거나 읽을 값의 최대 크기를 결정할 수 있습니다.  
  
 **매개 변수** 개체의 가변 길이 데이터 형식을 지정 하는 경우 (예: **AdVarChar**등의 **문자열** 형식) [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션에 추가 하기 전에 개체의 **크기** 속성을 설정 해야 합니다. 그렇지 않으면 오류가 발생 합니다.  
  
 [Command](../../../ado/reference/ado-api/command-object-ado.md) 개체의 **Parameters** 컬렉션에 **매개 변수** 개체를 이미 추가 했 고 해당 형식을 가변 길이 데이터 형식으로 변경한 경우에는 **Command** 개체를 실행 하기 전에 **매개 변수** 개체의 **Size** 속성을 설정 해야 합니다. 그렇지 않으면 오류가 발생 합니다.  
  
 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드를 사용 하 여 공급자에서 매개 변수 정보를 가져오고 하나 이상의 가변 길이 데이터 형식 **매개 변수** 개체를 반환 하는 경우, ADO는 실행 중에 오류를 발생 시킬 수 있는 최대 크기를 기준으로 매개 변수에 대 한 메모리를 할당할 수 있습니다. 오류를 방지 하려면 명령을 실행 하기 전에 이러한 매개 변수의 **Size** 속성을 명시적으로 설정 해야 합니다.  
  
 **Size** 속성은 읽기/쓰기입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size 속성(ADO 스트림)](../../../ado/reference/ado-api/size-property-ado-stream.md)
