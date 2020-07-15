---
title: '예제: CDATA 지시어 지정 | Microsoft Docs'
description: CDATA 지시어를 지정하여 CDATA 섹션의 지정된 데이터를 래핑하는 방법 예제를 확인합니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- CDATA directive
ms.assetid: 949071e6-787f-480d-bb86-3ac16a027af1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e0c768d68c1bf7bb8d5c08b3967b4172fbdca36
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632626"
---
# <a name="example-specifying-the-cdata-directive"></a>예제: CDATA 지시어 지정
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
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
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
