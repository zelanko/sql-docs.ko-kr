---
title: "Parameter 개체가 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Parameter
helpviewer_keywords: Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7916c054b41b63b358f8330ff1a21b05689f2920
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="parameter-object"></a>Parameter 개체
매개 변수 또는 연결 된 인수를 나타냅니다는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 매개 변수가 있는 쿼리 또는 저장된 프로시저에 따라 개체입니다.  
  
## <a name="remarks"></a>주의  
 대부분의 공급자는 매개 변수가 있는 명령을 지원 합니다. 명령을 원하는 작업 정의 되어 있는 한 번은 이지만 변수 (또는 매개 변수)는 명령의 일부 세부 정보를 변경 하는 데 사용 합니다. 예를 들어 SQL SELECT 문을 WHERE 절 및 정렬 기준 절에 대 한 열 이름을 정의 하는 다른 일치 하는 조건을 정의 하는 매개 변수를 사용할 수 없습니다.  
  
 **매개 변수**  /out 인수 및 반환 값의 저장 프로시저 또는 개체 매개 변수가 있는 쿼리와 관련 된 매개 변수를 나타냅니다. 기능 공급자, 일부 컬렉션, 메서드 또는 속성에 따라 한 **매개 변수** 개체를 사용할 수 없습니다.  
  
 컬렉션, 메서드 및 속성의는 **매개 변수** 개체를 다음을 수행할 수 있습니다.  
  
-   매개 변수 이름을 설정 하거나 반환할는 [이름](../../../ado/reference/ado-api/name-property-ado.md) 속성입니다.  
  
-   설정 또는 반환 값 매개 변수는 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성입니다. **값** 은의 기본 속성은 **매개 변수** 개체입니다.  
  
-   설정 하거나와 매개 변수 특징을 반환할는 [특성](../../../ado/reference/ado-api/attributes-property-ado.md), [방향](../../../ado/reference/ado-api/direction-property.md), [정밀도](../../../ado/reference/ado-api/precision-property-ado.md), [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [ 크기](../../../ado/reference/ado-api/size-property-ado-parameter.md), 및 [형식](../../../ado/reference/ado-api/type-property-ado.md) 속성입니다.  
  
-   긴 이진 또는 문자 데이터와 매개 변수에 전달 된 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 메서드.  
  
-   공급자별 특성을 사용 하 여 액세스는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
 연결 된 매개 변수 속성을 이름을 알고 있는 경우 호출 하려는 저장된 프로시저 또는 매개 변수가 있는 쿼리를 사용할 수 있습니다는 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) 를 만들 방법을 **매개 변수** 개체 적절 한 속성 설정 및 사용 하 여 사용 된 [Append](../../../ado/reference/ado-api/append-method-ado.md) 메서드를 추가 하는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다. 이렇게 하면 설정 하 고 호출할 필요 없이 매개 변수 값을 반환할 수 있습니다는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드를는 **매개 변수** 컬렉션 매개 변수 정보는 공급자에서 검색 하는 잠재적으로 리소스 집약적 작업입니다.  
  
 **매개 변수** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [매개 변수 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Command 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter 메서드 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
