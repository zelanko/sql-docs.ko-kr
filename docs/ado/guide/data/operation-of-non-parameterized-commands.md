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
manager: craigg
ms.openlocfilehash: 884ef4e72b975de0eb9dd92e80ec3ce0d513546b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822151"
---
# <a name="operation-of-non-parameterized-commands"></a>매개 변수화되지 않은 명령 작업
매개 변수가 없는 명령에 대 한 모든 공급자 명령 실행 되 고 **레코드 집합** 명령 실행 하는 동안 만들어집니다. 명령은 동기적으로 실행 되는 경우 모든 합니다 **레코드 집합** 완전히 채울 수 있습니다. 비동기 채우기 모드가 선택 된 경우의 채워진된 상태를 **레코드 집합** 채우기 모드와 크기에 따라 달라 집니다 합니다 **레코드 집합**합니다.  
  
 예를 들어, 합니다 *상위 명령* 반환할 수 있습니다를 **레코드 집합** 고객 테이블에서 회사는 고객의 및 *자식* 를반환할수있습니다**레코드 집합** 는 Orders 테이블에서 모든 고객의 주문 합니다.  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 매개 변수가 없는 부모-자식 관계의 경우 각 부모 및 자식 **레코드 집합** 개체에 연결 하는 공통 열이 있어야 합니다. 해당 열이 RELATE 절에서 명명 *부모 열* 첫 번째 차례로 *자식 열*합니다. 열에 다른 이름을 가질 수 **레코드 집합** 개체 있지만 의미 있는 관계를 지정 하기 위해 동일한 정보를 참조 해야 합니다. 예를 들어 합니다 **고객** 하 고 **주문 레코드 집합** customerID 필드는 둘 다 개체. 때문에 자식 멤버 자격 **Recordset** 자식 공급자 명령에 의해 결정 됩니다 **레코드 집합** 분리 된 행을 포함할 수 있습니다. 이러한 분리 된 행에 액세스할 수 없는 추가 모양 변경 하지 않고 있습니다.  
  
 부모 장 열이 추가 데이터 셰이핑 **레코드 집합**합니다. 장 열 값은 자식에서 행에 대 한 참조가 **레코드 집합**, RELATE 절을 충족 하는 합니다. 즉, 동일한 값이에 *부모 열* 에 지정 된 부모 행의는 *자식 열* 장 자식의 모든 행. TO 절이 여러 개를 동일한 RELATE 절에서 사용 하는 경우 AND 연산자를 사용 하 여 암시적으로 결합 되어 있습니다. RELATE 절에서 부모 열인 부모 키를 구성 하지 않습니다 하는 경우 **레코드 집합**, 단일 자식 행을 여러 부모 행을 포함할 수 있습니다.  
  
 ADO를 자동으로 검색 장 열에 대 한 참조에 액세스 하는 경우는 **레코드 집합** 참조에 의해 표현 합니다. 하지만 매개 변수가 없는 명령에서 유의 전체 자식 **레코드 집합** 되었습니다 검색만 제공 합니다 행의 하위 집합입니다.  
  
 추가 된 열이 없으면 *장-별칭*, 이름에 대 한에 자동으로 생성 합니다. A [필드](../../../ado/reference/ado-api/field-object.md) 열에 추가할 개체를 **레코드 집합** 개체의 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션 및 데이터 형식과 **adChapter**.  
  
 계층적 탐색에 대 한 자세한 **레코드 집합**를 참조 하세요 [계층적 레코드 집합에서 행 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)   
 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
