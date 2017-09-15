---
title: "명령 속성-동적 (ADO)를 다시 동기화 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cfa4fee83eef9c17a7dfb1eae6dbad64be2c98ce
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="resync-command-property-dynamic-ado"></a>명령 속성-동적 (ADO)를 다시 동기화
지정 된 사용자가 제공한 명령 문자열의 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 에 명명 된 테이블의 데이터를 새로 고치려면 메서드 문제는 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 동적 속성.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 명령 문자열에 해당 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체는 여러 기본 테이블에서 실행 하는 JOIN 연산의 결과입니다. 영향을 받는 행에 따라 달라 집니다는 *AffectRecords* 의 매개 변수는 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드. 표준 **다시 동기화** 경우 메서드가 실행 되는 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 및 **Resync Command** 속성이 설정 되지 않은 합니다.  
  
 명령 문자열은 **Resync Command** 속성 매개 변수가 있는 명령 또는 저장된 프로시저를 새로 고치는 행을 고유 하 게 식별 하 고 행으로 동일한 수와 열 순서를 포함 하는 단일 행을 반환 새로 고쳐집니다. 각 기본 키 열에 대 한 매개 변수를 포함 하는 명령 문자열의 **고유 테이블**, 그렇지 않으면 런타임에 오류가 반환 됩니다. 매개 변수를 새로 고칠 수 있는 행의 기본 키 값을 사용 하 여 자동으로 채워집니다.  
  
 SQL에 기반 하는 두 가지 예는 다음과 같습니다.  
  
 1\) 는 **레코드 집합** 명령에 의해 정의 됩니다.  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 **Resync Command** 속성:  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 **고유 테이블** 은 *Orders* 와 기본 키가 *OrderID*, 매개 변수화 합니다. 하위 select를 프로그래밍 방식으로 동일한 수와 열 순서는 원래 명령에 의해 반환 되도록 보장 하는 간단한 방법을 제공 합니다.  
  
 2\) 는 **레코드 집합** 저장된 프로시저에 의해 정의 됩니다.  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 **Resync** 메서드에서 다음 저장된 프로시저를 실행 해야 합니다.  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 **Resync Command** 속성:  
  
```  
"{call CustordersResync (?)}"  
```  
  
 다시 한 번는 **고유 테이블** 은 *Orders* 와 기본 키가 *OrderID*, 매개 변수화 합니다.  
  
 **다시 동기화 명령** 동적 속성에 추가 **레코드 집합** 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 때는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성 **adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
