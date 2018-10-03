---
title: 데이터 셰이핑 예제 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92e34de1b9fd675570527f9a28f8476a51597f10
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696431"
---
# <a name="data-shaping-example"></a>데이터 셰이핑 예제
다음 데이터 셰이핑 명령 계층을 구축 하는 방법을 보여 줍니다 **레코드 집합** 에서 **고객** 하 고 **주문** Northwind 데이터베이스의 테이블입니다.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 열려는이 명령을 사용 하면를 **레코드 집합** 개체 (에서처럼 [데이터 셰이핑의 Visual Basic 예제](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)), 장에 만듭니다 (**chapOrders**) 반환 된 각 레코드에 대 한 **고객** 테이블입니다. 이 챕터의 하위 집합으로 구성 됩니다는 **레코드 집합** 에서 반환 되는 **주문** 테이블입니다. 합니다 **chapOrders** 장 지정 된 고객의 주문에 대 한 모든 요청 된 정보를 포함 합니다. 이 예제에서는 장 열으로 구성 3: **OrderID**를 **OrderDate**, 및 **CustomerID**합니다.  
  
 모양 결과의 처음 두 항목은 **레코드 집합** 는 다음과 같습니다.  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 셰이프 명령에서 추가 만드는 데 사용 되는 자식 **레코드 집합** 부모 관련이 **레코드 집합** (셰이프 키워드를 실행해봤습니다 직후 공급자별 명령에서 반환 됨 RELATE 절에서 이전). 부모 및 자식 일반적으로 하나 이상의 열에 공통점이: 부모 행의 열 값은 모든 자식 행의 열 값과 동일 합니다.  
  
 셰이프 명령을 사용 하 여 두 번째 방법이 있습니다: 즉, 부모를 생성 하 **레코드 집합** 자식에서 **레코드 집합**합니다. 자식에서 레코드 **Recordset** 그룹화 되며, 일반적으로 BY 절과 한 개의 행을 사용 하 여 추가할 부모 **레코드 집합** 결과 각 그룹의 자식에 대 한 합니다. BY 절을 생략 하는 경우 자식 **Recordset** 단일 그룹 및 부모 폼은 **레코드 집합** 정확히 하나의 행이 포함 됩니다. 전체 자식 "총합계" 집계를 계산할 유용 **레코드 집합**합니다.  
  
 셰이프 명령 구문을 만들 수 있습니다 프로그래밍 방식으로 모양의 **레코드 집합**합니다. 구성 요소에 액세스할 수 있습니다 합니다 **레코드 집합** 프로그래밍 방식으로 또는 적절 한 시각적 컨트롤을 통해. 다른 ADO 명령 텍스트와 같은 셰이프 명령을 발급 됩니다. 자세한 내용은 [셰이프는 일반적 명령](../../../ado/guide/data/shape-commands-in-general.md)입니다.  
  
 방식에 관계 없이 부모 **Recordset** 는 형식이 포함 됩니다 장 열을 자식으로 연결 하는 데 사용 되는 **레코드 집합**합니다. 원할 경우 부모 **레코드 집합** 자식 행에 대해 집계 (SUM, MIN, MAX 및 등)를 포함 하는 열 수도 있습니다. 부모와 자식 **레코드 집합** 행이 행에서 식을 포함 하는 열이 있을 수 있습니다 합니다 **레코드 집합**뿐 아니라 새 및 처음에 열에서 빈 합니다.  
  
 이 섹션에서는 다음 항목을 사용 하 여 계속합니다.  
  
-   [데이터 셰이핑의 Visual Basic 예제](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
