---
title: '예: ELEMENTS 지시어를 사용하여 XSINIL 지정 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying XSINIL example
ms.assetid: 07c873ff-1f9d-480e-8536-862c39eb8249
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34cc4479a26d633e689963a945095248f683993f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287283"
---
# <a name="example-specifying-xsinil-with-the-elements-directive"></a>예: ELEMENTS 지시어를 사용하여 XSINIL 지정
  다음 쿼리는 `ELEMENTS` 지시어를 지정하여 쿼리 결과로부터 요소 중심 XML을 생성합니다.  
  
## <a name="example"></a>예제  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<row>  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
 `Color` 열에 일부 제품에 대해 Null 값이 있기 때문에 결과 XML은 해당 <`Color`> 요소를 생성하지 않습니다. `XSINIL` 지시어를 `ELEMENTS`와 함께 추가하면 NULL 색상 값에 대해서도 <`Color`> 요소를 결과 집합에 생성할 수 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS XSINIL ;  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
  <Color xsi:nil="true" />  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 RAW 모드 사용](use-raw-mode-with-for-xml.md)  
  
  
