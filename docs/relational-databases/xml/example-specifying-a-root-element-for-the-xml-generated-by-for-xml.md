---
title: "예제: FOR XML로 생성된 XML에 대한 루트 요소 지정 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RAW mode, specifying root element example
- RAW mode, with FOR XML example
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b29b195a3bff00b3c277767df4d18a0d001eb9ed
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="example-specifying-a-root-element-for-the-xml-generated-by-for-xml"></a>예제: FOR XML로 생성된 XML에 대한 루트 요소 지정
  `ROOT` 쿼리에 `FOR XML` 옵션을 지정하면 이 쿼리에 표시된 것과 같이 결과 XML에 대해 단일 최상위 요소를 요청할 수 있습니다. `ROOT` 지시어에 지정된 인수는 루트 요소 이름을 제공합니다.  
  
## <a name="example"></a>예제  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
go  
```  
  
 다음은 결과입니다.  
  
```  
<MyRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
  <row ProductModelID="115" Name="Cable Lock" />  
</MyRoot>  
```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  

