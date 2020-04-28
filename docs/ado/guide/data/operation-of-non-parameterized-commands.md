---
title: 매개 변수가 없는 명령의 작업 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3512b484425749ed027f6533dab7398765c1af2e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924745"
---
# <a name="operation-of-non-parameterized-commands"></a>매개 변수화되지 않은 명령 작업
매개 변수가 없는 명령의 경우 모든 공급자 명령이 실행 되 고 명령을 실행 하는 동안 **레코드 집합이** 생성 됩니다. 명령이 동기적으로 실행 되는 경우 모든 **레코드 집합** 은 완전히 채워집니다. 비동기 채우기 모드가 선택 된 경우 **레코드 집합** 의 채워진 상태는 채우기 모드와 **레코드 집합**의 크기에 따라 달라 집니다.  
  
 예를 들어, *부모 명령은* customers 테이블에서 회사에 대 한 고객의 **레코드 집합** 을 반환할 수 있으며, *하위 명령은* orders 테이블의 모든 고객에 대 한 주문 **레코드 집합** 을 반환할 수 있습니다.  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 매개 변수가 없는 부모-자식 관계의 경우 각 부모 및 자식 **레코드 집합** 개체를 연결 하려면 공통 된 열이 있어야 합니다. 이 열은 RELATE 절, *부모-열* 에 먼저 이름이 지정 된 다음 *하위 열*로 지정 됩니다. 해당 **레코드 집합** 개체에는 열 이름이 서로 다를 수 있지만 의미 있는 관계를 지정 하기 위해 동일한 정보를 참조 해야 합니다. 예를 들어 **Customers** 및 **Orders 레코드 집합** 개체는 모두 customerID 필드를 가질 수 있습니다. 자식 **레코드 집합** 의 멤버 자격은 공급자 명령에 의해 결정 되기 때문에 자식 **레코드 집합** 에는 분리 된 행이 포함 될 수 있습니다. 이러한 분리 된 행은 추가 변형 없이 액세스할 수 없습니다.  
  
 데이터 셰이핑은 부모 **레코드 집합**에 장 열을 추가 합니다. Chapter 열의 값은 RELATE 절을 충족 하는 자식 **레코드 집합**의 행에 대 한 참조입니다. 즉, 동일한 값이 지정 된 부모 행의 *부모-열* 에 장 자식의 모든 행에 있는 *자식 열* 에 있는 것과 동일한 값입니다. 동일한 RELATE 절에서 여러 TO 절을 사용 하는 경우 AND 연산자를 사용 하 여 암시적으로 결합 됩니다. RELATE 절의 부모 열이 부모 **레코드 집합**에 대 한 키를 구성 하지 않는 경우 단일 자식 행에 여러 개의 부모 행이 있을 수 있습니다.  
  
 장 열에서 참조에 액세스 하면 ADO에서 참조로 표시 되는 **레코드 집합** 을 자동으로 검색 합니다. 매개 변수가 없는 명령에서 전체 하위 **레코드 집합이** 검색 되더라도이 장은 행의 하위 집합만을 제공 합니다.  
  
 추가 된 열에 *장 별칭이*없으면 자동으로 이름이 생성 됩니다. 열에 대 한 [Field](../../../ado/reference/ado-api/field-object.md) 개체가 **레코드 집합** 개체의 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 추가 되 고 해당 데이터 형식은 **adchapter**가 됩니다.  
  
 계층적 **레코드 집합**을 탐색 하는 방법에 대 한 자세한 내용은 [계층적 레코드 집합의 행에 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예](../../../ado/guide/data/data-shaping-example.md)   
 [공식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
