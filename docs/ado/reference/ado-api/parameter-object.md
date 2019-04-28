---
title: 매개 변수 개체 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e4a39f93e6b98595270e46d5a6f9b54b35098cb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710347"
---
# <a name="parameter-object"></a>Parameter 개체
매개 변수 또는 연결 된 인수를 나타내는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 매개 변수가 있는 쿼리 또는 저장된 프로시저를 기반으로 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 대부분의 공급자에 매개 변수가 있는 명령을 지원합니다. 이러한 명령을 원하는 작업을 한 번 정의는 되지만 변수 (또는 매개 변수)는 명령의 일부 세부 정보를 변경 하는 데 사용 합니다. 예를 들어 SQL SELECT 문을 WHERE 절 및 정렬 기준 절에 열 이름을 정의 하는 다른 일치 하는 조건을 정의 하는 매개 변수를 사용할 수 없습니다.  
  
 **매개 변수** 입/출력 인수 및 반환 값에 대 한 저장 프로시저 또는 개체 매개 변수가 있는 쿼리를 사용 하 여 연결 된 매개 변수를 나타냅니다. 공급자, 몇 가지 컬렉션, 메서드 또는 속성의 기능에 따라 한 **매개 변수** 개체를 사용할 수 없습니다.  
  
 컬렉션, 메서드 및 속성을 사용 하 여는 **매개 변수** 개체를 다음을 수행할 수 있습니다.  
  
-   설정 하거나 사용 하 여 매개 변수의 이름을 반환 합니다 [이름을](../../../ado/reference/ado-api/name-property-ado.md) 속성입니다.  
  
-   설정 하거나 사용 하 여 매개 변수의 값을 반환 합니다 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성입니다. **값** 의 기본 속성을 **매개 변수** 개체입니다.  
  
-   설정 하거나 매개 변수 특징을 반환 합니다 [특성](../../../ado/reference/ado-api/attributes-property-ado.md), [방향](../../../ado/reference/ado-api/direction-property.md)를 [정밀도](../../../ado/reference/ado-api/precision-property-ado.md)를 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [ 크기](../../../ado/reference/ado-api/size-property-ado-parameter.md), 및 [형식](../../../ado/reference/ado-api/type-property-ado.md) 속성입니다.  
  
-   긴 이진 또는 문자 데이터를 사용 하 여 매개 변수에 전달 된 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 메서드.  
  
-   공급자별 특성을 사용 하 여 액세스 합니다 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
 연결 된 매개 변수의 속성을 이름이 알고 있는 경우 호출 하려는 저장된 프로시저 또는 매개 변수가 있는 쿼리를 사용할 수 있습니다 합니다 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) 메서드를 만듭니다 **매개 변수** 개체 사용 하 여 확인 하 고 적절 한 속성 설정을 사용 하 여는 [추가](../../../ado/reference/ado-api/append-method-ado.md) 메서드를 추가 합니다 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션. 이렇게 하면 설정 하 고 호출 하지 않고 매개 변수 값을 반환할 수 있습니다는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드는 **매개 변수** 공급자에서 매개 변수 정보를 검색할 컬렉션을 잠재적으로 리소스 집약적 작업입니다.  
  
 합니다 **매개 변수** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [매개 변수 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [명령 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter 메서드 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
