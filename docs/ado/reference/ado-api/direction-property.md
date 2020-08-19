---
description: Direction 속성
title: Direction 속성 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 37987e58829b1b6957b4fe1de440aaeb4aae1763
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444055"
---
# <a name="direction-property"></a>Direction 속성
[매개](../../../ado/reference/ado-api/parameter-object.md) 변수가 입력 매개 변수, 출력 매개 변수, 입력 및 출력 매개 변수를 나타내는지, 아니면 저장 프로시저의 반환 값 인지를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Direction** 속성을 사용 하 여 프로시저에 매개 변수를 전달 하는 방법을 지정 합니다. **Direction** 속성은 읽기/쓰기입니다. 이렇게 하면 ADO에서 매개 변수 정보를 검색 하는 공급자에 대 한 추가 호출을 수행 하지 않을 때이 정보를 반환 하지 않거나이 정보를 설정 하지 않는 공급자 작업을 수행할 수 있습니다.  
  
 모든 공급자가 저장 프로시저의 매개 변수 방향을 결정할 수 있는 것은 아닙니다. 이러한 경우 쿼리를 실행 하기 전에 **방향** 속성을 설정 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
