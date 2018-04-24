---
title: Direction 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1644923b3bd61290a2c6afc407172e8bb9fa7143
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="direction-property"></a>Direction 속성
나타냅니다 여부는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 입력된 매개 변수, 출력 매개 변수, 입력 및 출력 매개 변수를 나타내는 매개 변수가 저장된 프로시저에서 반환 값 이면 또는 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **방향** 속성 또는 프로시저에서 매개 변수가 전달 되는 방법을 지정 합니다. **방향** 속성은 읽기/쓰기; 이렇게 하면이 정보를 반환 하지 않는 공급자와 함께 작동 하도록 하거나 매개 변수 정보를 검색 하는 공급자에 게 추가 호출을 수행 하는 ADO를 원치 않는 경우이 정보를 설정 합니다.  
  
 일부 공급자는 저장된 프로시저에서 매개 변수의 방향을 확인할 수 있습니다. 이러한 경우에 설정 해야 합니다는 **방향** 쿼리를 실행 하기 전에 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
