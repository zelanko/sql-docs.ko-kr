---
description: Resync Command 속성-동적(ADO)
title: Resync Command 속성-Dynamic (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e882a9c65bf0d54dc9bd9e160edbc67f4e7996b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989514"
---
# <a name="resync-command-property-dynamic-ado"></a>Resync Command 속성-동적(ADO)
[Resync](./resync-method.md) 메서드에서 [고유 테이블](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 동적 속성의 테이블에 있는 데이터를 새로 고치는 데 발급 하는 사용자 제공 명령 문자열을 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 명령 문자열인 **문자열** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 [레코드 집합](./recordset-object-ado.md) 개체는 여러 기본 테이블에 대해 실행 된 조인 작업의 결과입니다. 영향을 받는 행은 [Resync](./resync-method.md) 메서드의 *AffectRecords* 매개 변수에 따라 달라 집니다. [고유 테이블](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 및 다시 **동기화 명령** 속성을 설정 하지 않으면 표준 다시 **동기화** 방법이 실행 됩니다.  
  
 **Resync command** 속성의 명령 문자열은 새로 고칠 행을 고유 하 게 식별 하는 매개 변수가 있는 명령 또는 저장 프로시저 이며, 새로 고칠 행과 동일한 수와 순서를 포함 하는 단일 행을 반환 합니다. 명령 문자열은 **고유 테이블**의 각 기본 키 열에 대 한 매개 변수를 포함 합니다. 그렇지 않으면 런타임 오류가 반환 됩니다. 매개 변수는 새로 고칠 행의 기본 키 값으로 자동으로 채워집니다.  
  
 다음은 SQL을 기반으로 하는 두 가지 예제입니다.  
  
 1 \) **레코드 집합** 은 명령으로 정의 됩니다.  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 **Resync 명령** 속성은 다음과 같이 설정 됩니다.  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 **고유 테이블** 은 *Orders* 이 고 해당 기본 키인 *OrderID*는 매개 변수화 됩니다. 하위 select는 원래 명령과 동일한 개수의 열이 반환 되는지 프로그래밍 방식으로 확인 하는 간단한 방법을 제공 합니다.  
  
 2 \) **레코드 집합** 은 저장 프로시저에 의해 정의 됩니다.  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 **Resync** 메서드는 다음 저장 프로시저를 실행 해야 합니다.  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 **Resync 명령** 속성은 다음과 같이 설정 됩니다.  
  
```  
"{call CustordersResync (?)}"  
```  
  
 이 경우 **고유 테이블** 은 *Orders* 이 고 기본 키인 *OrderID*는 매개 변수화 됩니다.  
  
 **Resync 명령은** [CursorLocation](./cursorlocation-property-ado.md) 속성이 **AdUseClient**로 설정 된 경우 **레코드 집합** 개체 [속성](./properties-collection-ado.md) 컬렉션에 추가 되는 동적 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)