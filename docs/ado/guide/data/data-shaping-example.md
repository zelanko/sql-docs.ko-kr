---
title: "데이터 예제를 셰이핑 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7b6719d8cdd2c86482c3c125ceec52fafdf3e397
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="data-shaping-example"></a>데이터 예제를 셰이핑
다음 데이터 셰이핑 명령을 계층적 구조를 작성 하는 방법을 보여 줍니다 **레코드 집합** 에서 **고객** 및 **Orders** Northwind 데이터베이스의 테이블입니다.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 열려면이 명령을 사용 하면 한 **레코드 집합** 개체 (에 표시 된 대로 [데이터 셰이핑의 Visual Basic 예제](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)), 장에 만듭니다 (**chapOrders**) 반환 하는 각 레코드에 대 한 **고객** 테이블입니다. 하위 집합으로 이루어져이 장에서 **레코드 집합** 에서 반환 되는 **Orders** 테이블입니다. **chapOrders** 장 지정 된 고객의 주문에 대 한 모든 요청 된 정보를 포함 합니다. 이 예제에서는 장의 열으로 구성 3: **OrderID**, **OrderDate**, 및 **CustomerID**합니다.  
  
 모양 결과의 처음 두 항목 **레코드 집합** 는 다음과 같습니다.  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|분석 Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 SHAPE 명령에 추가 자식을 만드는 데 사용 되 **레코드 집합** 부모와 관련 된 **레코드 집합** (설명한 셰이프 키워드 바로 다음 공급자별 명령에서 반환 됨 RELATE 절에서 이전). 부모 및 자식 일반적으로 서로 열을 하나 이상 공통: 부모 행의 열 값은 자식의 모든 행의 열 값과 동일 합니다.  
  
 셰이프 명령을 사용 하 여 두 번째 방법은: 즉, 부모를 생성 하려면 **레코드 집합** 자식에서 **레코드 집합**합니다. 하위 레코드 **레코드 집합** 그룹화 되며, 일반적으로 BY 절과 한 개의 행을 사용 하 여 추가할 부모 **레코드 집합** 하위에 있는 각 결과 그룹에 대 한 합니다. BY 절을 생략 하면 자식 **레코드 집합** 단일 그룹 및 부모 폼은 **레코드 집합** 정확히 한 개의 행이 포함 됩니다. 이것은 전체 자식 "총합계" 집계를 계산할 적합 **레코드 집합**합니다.  
  
 셰이프 명령 구문을 또한 프로그래밍 방식으로 만들 수는 셰이핑된 **레코드 집합**합니다. 구성 요소에 액세스할 수 있습니다는 **레코드 집합** 프로그래밍 방식으로 또는 적절 한 시각적 컨트롤을 통해. Shape 명령은 다른 ADO 명령 텍스트 처럼 발급 됩니다. 자세한 내용은 참조 [셰이프 일반적 명령을](../../../ado/guide/data/shape-commands-in-general.md)합니다.  
  
 어떤 방식으로 관계 없이 부모 **레코드 집합** 는 형식이 포함 됩니다 자식 관련 시키는 데 사용 되는 장 열 **레코드 집합**합니다. 원할 경우 부모 **레코드 집합** 자식 행에 대해 집계 (SUM, MIN, MAX, 및 등)를 포함 하는 열을 포함할 수도 있습니다. 부모와 자식 **레코드 집합** 의 행에는 식을 포함 하는 열이 있을 수는 **레코드 집합**뿐만 아니라 열 및 처음 새로운은 비어 있습니다.  
  
 이 섹션의 다음 항목으로 계속 됩니다.  
  
-   [데이터 셰이핑의 Visual Basic 예제](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
