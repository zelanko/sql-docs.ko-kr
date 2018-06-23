---
title: '예제: 제품 모델 정보를 XML로 검색 | Microsoft 문서'
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
- RAW mode, retrieving XML information example
ms.assetid: 3828b4ca-3ab2-444f-9c58-8be6e7f064a6
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6c6eead2a8016572cf8fe2491463fb396218e58f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092132"
---
# <a name="example-retrieving-product-model-information-as-xml"></a>예제: 제품 모델 정보를 XML로 검색
  다음 쿼리는 제품 모델 정보를 반환합니다. `RAW` 모드는 `FOR XML` 절에서 지정됩니다.  
  
## <a name="example"></a>예제  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW;  
GO  
```  
  
 다음은 결과의 일부입니다.  
  
 `<row ProductModelID="122" Name="All-Purpose Bike Stand" />`  
  
 `<row ProductModelID="119" Name="Bike Wash" />`  
  
 `ELEMENTS` 지시어를 지정하여 요소 중심 XML을 검색할 수 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 다음은 결과입니다.  
  
```  
<row>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</row>  
<row>  
  <ProductModelID>119</ProductModelID>  
  <Name>Bike Wash</Name>  
</row>  
```  
  
 선택적으로 지정할 수는 `TYPE` 으로 결과 검색 하는 지시문 `xml` 유형입니다. `TYPE` 지시어는 결과의 내용을 변경하지 않습니다. 결과의 데이터 형식에만 영향을 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, TYPE ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 RAW 모드 사용](use-raw-mode-with-for-xml.md)  
  
  