---
title: "Size 속성 (ADO 매개 변수) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 73a6f0f2cd2e0d59ba6cd3e581e9f2aab8934c5f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="size-property-ado-parameter"></a>Size 속성 (ADO 매개 변수)
바이트 또는 문자, 최대 크기를 나타냅니다는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **긴** 바이트 또는 문자 값의 최대 크기를 나타내는 값을 **매개 변수** 개체입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **크기** 에 기록 된 값에 대 한 최대 크기를 결정 하거나에서 읽은 속성의 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성의는 **매개 변수** 개체입니다.  
  
 가변 길이 데이터 형식을 지정 하는 경우는 **매개 변수** 개체 (예를 들어 모든 **문자열** 같은 입력 **집합이 있으므로 필요**), 개체의 설정 해야  **크기** 속성에 추가 하기 전에 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션, 그렇지 않으면 오류가 발생 합니다.  
  
 이미 추가 된 경우는 **매개 변수** 개체는 **매개 변수** 의 컬렉션은 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체 하 고 해당 형식을 가변 길이 데이터 형식으로 변경 해야 합니다. 설정의 **매개 변수** 개체의 **크기** 속성을 실행 하기 전에 **명령** 개체; 그렇지 않으면 오류가 발생 합니다.  
  
 사용 하는 경우는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 공급자에서 매개 변수 정보를 얻는 메서드를 하나 이상의 가변 길이 데이터 형식 반환 **매개 변수** 개체, ADO 따라 매개 변수에 대 한 메모리 할당 에 허용 된 최대 크기를 실행 하는 동안 오류가 발생할 수 있습니다. 오류를 방지 하려면 하면 명시적으로 설정 해야는 **크기** 명령을 실행 하기 전에 이러한 매개 변수에 대 한 속성입니다.  
  
 **크기** 속성은 읽기/쓰기가 가능 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size 속성(ADO 스트림)](../../../ado/reference/ado-api/size-property-ado-stream.md)

