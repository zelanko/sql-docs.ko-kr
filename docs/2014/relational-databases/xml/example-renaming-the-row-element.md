---
title: '예제: &lt;row&gt; 요소 이름 바꾸기 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
author: rothja
ms.author: jroth
ms.openlocfilehash: 867fafaa85e1113a60517311b789bd7cc47d19f0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048737"
---
# <a name="example-renaming-the-ltrowgt-element"></a>예제: &lt;row&gt; 요소 이름 바꾸기
  결과 집합의 각 행에 대해 RAW 모드는 `<row>`요소를 생성합니다. 이 쿼리에 표시된 것과 같이 RAW 모드에 선택적 인수를 지정하여 선택적으로 이 요소에 다른 이름을 지정할 수 있습니다. 이 쿼리는 행 집합의 각 행에 대해 <`ProductModel`> 요소를 반환합니다.  
  
## <a name="example"></a>예제  
  
```  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122  
FOR XML RAW ('ProductModel'), ELEMENTS  
GO  
```  
  
 다음은 결과입니다. 쿼리에 `ELEMENTS` 지시어가 추가되었기 때문에 결과는 요소 중심입니다.  
  
```  
<ProductModel>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</ProductModel>   
```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 RAW 모드 사용](use-raw-mode-with-for-xml.md)  
  
  
