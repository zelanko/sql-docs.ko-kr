---
title: Resync Command 속성-동적 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5567bf3cc460aac6abfc2979a14e124bfd9d4cac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789291"
---
# <a name="resync-command-property-dynamic-ado"></a>Resync Command 속성-동적(ADO)
사용자가 제공한 명령 문자열을 지정 합니다 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 에 지정 된 테이블에서 데이터를 새로 고치려면 메서드 문제를 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 동적 속성입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **문자열** 명령 문자열 값.  
  
## <a name="remarks"></a>Remarks  
 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체가 여러 기본 테이블에서 실행 하는 조인 작업의 결과입니다. 영향을 받는 행에 따라 달라 집니다 합니다 *AffectRecords* 의 매개 변수를 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드. 표준 **Resync** 경우 메서드가 실행 되기 합니다 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 및 **Resync Command** 속성이 설정 되지 않습니다.  
  
 명령 문자열을 **Resync Command** 매개 변수가 있는 명령 또는 저장된 프로시저를 새로 고쳐 행을 고유 하 게 식별 하는 속성과 같은 개수 및 열 순서를 행으로 포함 된 단일 행을 반환 새로 고쳐집니다. 명령 문자열의 각 기본 키 열에 대 한 매개 변수를 포함 합니다 **고유 테이블**고, 그렇지 않으면 런타임에 오류가 반환 됩니다. 매개 변수를 자동으로 새로 고쳐져 야 하는 행의 기본 키 값으로 채웁니다.  
  
 SQL을 사용 하는 두 가지 예는 다음과 같습니다.  
  
 1\) 는 **레코드 집합** 명령에 의해 정의 됩니다.  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 합니다 **Resync Command** 속성:  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 **고유 테이블** 는 *주문* 와 기본 키가 *OrderID*를 매개 변수화 됩니다. 하위 select에 프로그래밍 방식으로 동일한 개수 및 열 순서는 원래 명령에 의해 반환 되도록를 확인 하는 간단한 방법을 제공 합니다.  
  
 2\) 는 **레코드 집합** 저장된 프로시저에 의해 정의 됩니다.  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 합니다 **Resync** 메서드에서 다음 저장된 프로시저를 실행 해야 합니다.  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 합니다 **Resync Command** 속성:  
  
```  
"{call CustordersResync (?)}"  
```  
  
 이번에 **고유 테이블** 은 *주문* 와 기본 키가 *OrderID*, 매개 변수화 된 합니다.  
  
 **명령을 다시 동기화** 에 추가 하는 동적 속성을 **레코드 집합** 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 때 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성**adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
