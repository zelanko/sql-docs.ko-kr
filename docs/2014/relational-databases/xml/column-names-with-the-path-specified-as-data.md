---
title: 경로가 data()로 지정된 열 이름 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
author: rothja
ms.author: jroth
ms.openlocfilehash: 45e48e7addad583ef6a9b9efb8163f592f5c33bb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059539"
---
# <a name="column-names-with-the-path-specified-as-data"></a>경로가 data()로 지정된 열 이름
  열 이름으로 지정된 경로가 "data()"일 경우 생성된 XML에서 해당 값이 원자 값으로 처리됩니다. 직렬화의 다음 항목도 원자성 값이면 공백 문자가 XML에 추가됩니다. 이 특징은 목록 유형의 요소와 특성 값을 만들 때 유용합니다. 다음 쿼리는 제품 모델 ID, 이름 및 해당 제품 모델에 속한 제품 목록을 검색합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID       AS "@ProductModelID",  
       Name                 AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
      FOR XML PATH (''))    AS "@ProductIDs"  
FROM  Production.ProductModel  
WHERE ProductModelID= 7   
FOR XML PATH('ProductModelData');  
```  
  
 중첩 SELECT가 제품 ID 목록을 검색합니다. "data()"를 제품 ID에 대한 열 이름으로 지정합니다. PATH 모드에서는 행 요소 이름에 빈 문자열을 지정하므로 행 요소가 생성되지 않습니다. 대신 부모 SELECT의 <`ProductModelData`> 행 요소에 대한 ProductID 특성에 할당된 대로 값이 반환됩니다. 다음은 결과입니다.  
  
 `<ProductModelData ProductModelID="7"`  
  
 `ProductModelName="HL Touring Frame"`  
  
 `ProductIDs="885 887 888 889 890 891 892 893" />`  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 PATH 모드 사용](use-path-mode-with-for-xml.md)  
  
  
