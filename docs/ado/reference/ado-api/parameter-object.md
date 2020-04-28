---
title: Parameter 개체 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15df27e3dc48decf743a78dd4d147a22dc7cf276
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931668"
---
# <a name="parameter-object"></a>Parameter 개체
매개 변수가 있는 쿼리 또는 저장 프로시저를 기반으로 [Command](../../../ado/reference/ado-api/command-object-ado.md) 개체와 연결 된 매개 변수 또는 인수를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 많은 공급자가 매개 변수가 있는 명령을 지원 합니다. 이러한 명령은 원하는 작업을 한 번 정의 하지만 변수 (또는 매개 변수)를 사용 하 여 명령의 일부 세부 정보를 변경 하는 명령입니다. 예를 들어 SQL SELECT 문은 매개 변수를 사용 하 여 WHERE 절의 일치 조건을 정의 하 고 다른 매개 변수를 사용 하 여 SORT BY 절의 열 이름을 정의할 수 있습니다.  
  
 **매개 변수** 개체는 매개 변수가 있는 쿼리와 관련 된 매개 변수 또는 in/out 인수 및 저장 프로시저의 반환 값을 나타냅니다. 공급자의 기능에 따라 **매개 변수** 개체의 일부 컬렉션, 메서드 또는 속성을 사용 하지 못할 수도 있습니다.  
  
 **매개 변수** 개체의 컬렉션, 메서드 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](../../../ado/reference/ado-api/name-property-ado.md) 속성을 사용 하 여 매개 변수의 이름을 설정 하거나 반환 합니다.  
  
-   [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성을 사용 하 여 매개 변수의 값을 설정 하거나 반환 합니다. **Value** 는 **매개 변수** 개체의 기본 속성입니다.  
  
-   [특성](../../../ado/reference/ado-api/attributes-property-ado.md), [방향](../../../ado/reference/ado-api/direction-property.md), [전체 자릿수](../../../ado/reference/ado-api/precision-property-ado.md), [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [크기](../../../ado/reference/ado-api/size-property-ado-parameter.md)및 [유형](../../../ado/reference/ado-api/type-property-ado.md) 속성을 사용 하 여 매개 변수 특성을 설정 하거나 반환 합니다.  
  
-   [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 메서드를 사용 하 여 긴 이진 또는 문자 데이터를 매개 변수에 전달 합니다.  
  
-   [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 공급자별 특성에 액세스 합니다.  
  
 호출 하려는 저장 프로시저 또는 매개 변수가 있는 쿼리와 연결 된 매개 변수의 이름 및 속성을 알고 있는 경우 [Createparameter](../../../ado/reference/ado-api/createparameter-method-ado.md) 메서드를 사용 하 여 적절 한 속성 설정을 사용 하 여 **매개 변수** 개체를 만들고 [Append](../../../ado/reference/ado-api/append-method-ado.md) 메서드를 사용 하 여 [매개](../../../ado/reference/ado-api/parameters-collection-ado.md) 변수 컬렉션에 추가할 수 있습니다. 이렇게 하면 리소스를 많이 사용 하는 작업 인 공급자에서 매개 변수 정보를 검색 하기 위해 **Parameters** 컬렉션에서 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드를 호출 하지 않고도 매개 변수 값을 설정 하 고 반환할 수 있습니다.  
  
 **매개 변수** 개체는 스크립팅에 안전 하지 않습니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [매개 변수 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Command 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter 메서드 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
