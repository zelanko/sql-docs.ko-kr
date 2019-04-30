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
manager: craigg
ms.openlocfilehash: 682a7aa30596af8a3727eec0daaba4e9fd412ac4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192832"
---
# <a name="size-property-ado-parameter"></a>Size 속성(ADO 매개 변수)
최대 크기를 바이트 또는 문자를 나타냅니다는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 **긴** 바이트 또는 문자 값의 최대 크기를 나타내는 값을 **매개 변수** 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **크기** 에서 읽거나 쓸 값에 대 한 최대 크기를 결정 하는 속성을 [값](../../../ado/reference/ado-api/value-property-ado.md) 의 속성을 **매개 변수** 개체.  
  
 에 대 한 가변 길이 데이터 형식을 지정 하는 경우는 **매개 변수** 개체 (예를 들어 모든 **문자열** 와 같이 입력 **집합이 있으므로 필요**), 개체를 설정 해야 합니다  **크기** 를 추가 하기 전에 속성을 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션 그렇지 않으면 오류가 발생 합니다.  
  
 이미 추가한 경우는 **매개 변수** 개체를 **매개 변수** 의 컬렉션을 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체 형식과 가변 길이 데이터 형식으로 변경 해야 합니다 설정 합니다 **매개 변수** 개체의 **크기** 실행 하기 전에 속성을 **명령** 개체. 그렇지 않으면 오류가 발생 합니다.  
  
 사용 하는 경우는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 공급자에서 매개 변수 정보를 얻는 메서드를 하나 이상의 가변 길이 데이터 형식 반환 **매개 변수** 개체, ADO 기반 매개 변수에 대 한 메모리를 할당할 수 있습니다 에 허용 된 최대 크기를 실행 하는 동안 오류가 발생할 수 있습니다. 오류를 방지 하려면 하면 명시적으로 설정 해야 합니다 **크기** 명령을 실행 하기 전에 이러한 매개 변수에 대 한 속성입니다.  
  
 합니다 **크기** 속성은 읽기/쓰기가 가능 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size 속성(ADO 스트림)](../../../ado/reference/ado-api/size-property-ado-stream.md)
