---
title: 데이터 셰이핑 예 | Microsoft Docs
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
ms.openlocfilehash: a946329ad95a2b226f186e571152268baa5f37c3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925663"
---
# <a name="data-shaping-example"></a>데이터 셰이핑 예제
다음 데이터 셰이핑 명령은 Northwind 데이터베이스의 **Customers** 및 **Orders** 테이블에서 계층적 **레코드 집합** 을 작성 하는 방법을 보여 줍니다.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 [데이터 셰이핑의 Visual Basic 예제](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)와 같이이 명령을 사용 하 여 **레코드 집합** 개체를 열면 **Customers** 테이블에서 반환 되는 각 레코드에 대해 챕터 (**chapOrders**)가 생성 됩니다. 이 장은 **Orders** 테이블에서 반환 되는 **레코드 집합** 의 하위 집합으로 구성 됩니다. **ChapOrders** 챕터에는 지정 된 고객에 의해 배치 된 주문에 대 한 모든 요청 된 정보가 포함 됩니다. 이 예제에서 장은 **OrderID**, **OrderDate**및 **CustomerID**의 세 열로 구성 됩니다.  
  
 결과로 만들어진 **레코드 집합** 의 처음 두 항목은 다음과 같습니다.  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|민 Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo ...|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 SHAPE 명령에서 APPEND는 RELATE 절에서 부모 **레코드 집합과** 관련 된 자식 **레코드 집합** 을 만드는 데 사용 됩니다. 앞에서 설명한 SHAPE 키워드 바로 다음에 오는 공급자별 명령에서 반환 됩니다. 부모 및 자식에는 일반적으로 일반적으로 하나 이상의 열이 있습니다. 부모 행의 열 값은 자식의 모든 행에 있는 열 값과 동일 합니다.  
  
 셰이프 명령을 사용 하는 두 번째 방법이 있습니다. 즉, 자식 **레코드 집합**에서 부모 **레코드 집합** 을 생성 합니다. 자식 **레코드 집합** 의 레코드는 일반적으로 by 절을 사용 하 여 그룹화 되며 자식에 있는 각 결과 그룹의 부모 **레코드 집합** 에 하나의 행이 추가 됩니다. BY 절을 생략 하면 자식 **레코드 집합** 은 단일 그룹을 형성 하 고 부모 **레코드 집합** 에는 정확히 한 개의 행이 포함 됩니다. 이는 전체 하위 **레코드 집합**에 대 한 "총합계" 집계를 계산 하는 데 유용 합니다.  
  
 셰이프 명령 구문을 사용 하 여 프로그래밍 방식으로 셰이프 **레코드 집합**을 만들 수도 있습니다. 그런 다음 프로그래밍 방식으로 또는 적절 한 시각적 컨트롤을 통해 **레코드 집합** 의 구성 요소에 액세스할 수 있습니다. Shape 명령은 다른 ADO 명령 텍스트와 같이 실행 됩니다. 자세한 내용은 [일반적으로 Shape 명령](../../../ado/guide/data/shape-commands-in-general.md)을 참조 하세요.  
  
 부모 **레코드 집합** 의 구성 방식에 관계 없이 자식 **레코드**집합에 연결 하는 데 사용 되는 챕터 열이 포함 됩니다. 원하는 경우 부모 **레코드 집합** 에는 자식 행에 대 한 집계 (SUM, MIN, MAX 등)가 포함 된 열이 포함 될 수도 있습니다. 부모 및 자식 **레코드 집합** 모두에는 **레코드 집합**의 행에 식이 포함 된 열이 포함 될 수 있으며 처음에는 비어 있는 열도 포함 될 수 있습니다.  
  
 이 섹션에서는 다음 항목을 계속 진행 합니다.  
  
-   [데이터 셰이핑의 Visual Basic 예제](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
