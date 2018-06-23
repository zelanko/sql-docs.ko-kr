---
title: '예제: ID 및 IDREFS 지시어 지정 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IDREFS directive
- ID directive
ms.assetid: 99b9f0d8-ecbb-4225-859f-881066c09785
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: efaa7da1a6e198f4e8fc122df0b7fe0360f625b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078564"
---
# <a name="example-specifying-the-id-and-idrefs-directives"></a>예제: ID 및 IDREFS 지시어 지정
  요소 특성으로 지정할 수는 `ID` type 특성 및 `IDREFS` 특성 참조 하는 데 사용할 수 있습니다. 이러한 방식은 문서 간 연결을 설정하며 관계형 데이터베이스의 기본 키 및 외래 키 관계와 비슷합니다.  
  
 이 예에서는 `ID` 및 `IDREFS` 지시어를 사용하여 `ID` 및 `IDREFS` 유형의 특성을 만드는 방법을 보여 줍니다. ID는 정수 값일 수 없기 때문에 이 예에서는 ID 값이 변환됩니다. 즉, 다른 유형으로 캐스팅됩니다. ID 값에는 접두사가 사용됩니다.  
  
 다음과 같이 XML을 생성한다고 가정해 보십시오.  
  
```  
<Customer CustomerID="C1" SalesOrderIDList=" O11 O22 O33..." >  
    <SalesOrder SalesOrderID="O11" OrderDate="..." />  
    <SalesOrder SalesOrderID="O22" OrderDate="..." />  
    <SalesOrder SalesOrderID="O33" OrderDate="..." />  
    ...  
</Customer>  
```  
  
 < `SalesOrderIDList` > 요소의 `Customer` 특성은 < `SalesOrderID` > 요소의 `SalesOrder` 특성을 참조하는 다중 값 특성입니다. 이 연결을 구성하려면 `SalesOrderID` 특성이 `ID` 유형으로 선언되어야 하며 <`Customer`> 요소의 `SalesOrderIDList` 특성이 `IDREFS` 유형으로 선언되어야 합니다. 한 고객이 여러 개의 주문을 요청할 수 있으므로 `IDREFS` 유형이 사용됩니다.  
  
 `IDREFS` 유형의 요소에는 또한 두 개 이상의 값이 포함됩니다. 따라서 같은 태그, 부모 및 키 열 정보를 다시 사용하는 별개의 SELECT 절을 사용해야 합니다. 그런 다음 `ORDER BY`에서 `IDREFS` 값을 구성하는 행 시퀀스가 해당 부모 요소 아래에 함께 표시되도록 해야 합니다.  
  
 이 쿼리는 원하는 XML을 생성합니다. 이 쿼리는 `ID` 및 `IDREFS` 지시어를 사용하여 열 이름(`SalesOrder!2!SalesOrderID!ID`, `Customer!1!SalesOrderIDList!IDREFS`)에 있는 유형을 덮어씁니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID       [Customer!1!CustomerID],  
        NULL               [Customer!1!SalesOrderIDList!IDREFS],  
        NULL               [SalesOrder!2!SalesOrderID!ID],  
        NULL               [SalesOrder!2!OrderDate]  
FROM   Sales.Customer C   
UNION ALL   
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID,  
        'O-'+CAST(SalesOrderID as varchar(10)),   
        NULL,  
        NULL  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
        C.CustomerID,  
        NULL,  
        'O-'+CAST(SalesOrderID as varchar(10)),  
        OrderDate  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerIDORDER BY [Customer!1!CustomerID] ,  
         [SalesOrder!2!SalesOrderID!ID],  
         [Customer!1!SalesOrderIDList!IDREFS]  
FOR XML EXPLICIT;  
```  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 EXPLICIT 모드 사용](use-explicit-mode-with-for-xml.md)  
  
  