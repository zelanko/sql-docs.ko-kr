---
title: '예제: CDATA 지시어 지정 | Microsoft 문서'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- CDATA directive
ms.assetid: 949071e6-787f-480d-bb86-3ac16a027af1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 050cf86e0f4a73aadb62b63ecccf46d69b78535f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094883"
---
# <a name="example-specifying-the-cdata-directive"></a>예제: CDATA 지시어 지정
  지시어가 **CDATA**로 설정되면 포함된 데이터가 엔터티 인코딩되지는 않지만 CDATA 섹션에 놓여집니다. **CDATA** 특성은 이름이 없어야 합니다.  
  
 다음 쿼리는 제품 모델 요약 설명을 CDATA 섹션에 포함시킵니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        '<Summary>This is summary description</Summary>'     
            as [ProductModel!1!!CDATA] -- no attribute name so ELEMENT assumed  
FROM    Production.ProductModel  
WHERE   ProductModelID=19  
FOR XML EXPLICIT  
```  
  
 다음은 결과입니다.  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
   <![CDATA[<Summary>This is summary description</Summary>]]>  
</ProductModel>  
```  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 EXPLICIT 모드 사용](use-explicit-mode-with-for-xml.md)  
  
  
