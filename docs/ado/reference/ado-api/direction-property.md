---
title: Direction 속성이 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 244cf01b2845e7f5ef6729efd9ea7a7cfa6b994c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695421"
---
# <a name="direction-property"></a>Direction 속성
나타냅니다 여부를 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 입력된 매개 변수, 출력 매개 변수, 입력 및 출력 매개 변수를 나타내는 매개 변수는 저장된 프로시저에서 반환 하는 경우.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **방향** 하거나 프로시저에서 매개 변수에서 전달 하는 방법을 지정 하는 속성입니다. **방향** 속성은 읽기/쓰기, 이렇게 하면이 정보를 반환 하지 않는 공급자와 함께 작동 하거나 매개 변수 정보를 검색할 공급자에 게는 추가 호출을 수행 하는 ADO를 표시 하지 않으려는 경우이 정보를 설정 합니다.  
  
 일부 공급자는 저장된 프로시저에서 매개 변수의 방향을 결정할 수 있습니다. 이러한 경우에 설정 해야 합니다 **방향을** 쿼리를 실행 하기 전에 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
