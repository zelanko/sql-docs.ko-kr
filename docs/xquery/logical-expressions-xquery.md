---
title: 논리 식 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- logical operators [SQL Server], XQuery
- effective Boolean value [XQuery]
- logical expressions [XQuery]
- EBV
- expressions [XQuery], logical
ms.assetid: de94cd2e-2d48-49fb-9ebd-a2d90c79bf62
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b1dc7b961dd0b85824ea180cbc4815d5488a360
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004500"
---
# <a name="logical-expressions-xquery"></a>논리 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 지원 논리 **하 고** 하 고 **또는** 연산자입니다.  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 테스트 식 `expression1,``expression2`의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 빈 시퀀스, 하나 이상의 노드 시퀀스 또는 단일 부울 값에서 발생할 수 있습니다. 결과를 바탕으로 유효한 해당 부울 값은 다음 방식으로 결정됩니다.  
  
-   테스트 식 결과 빈 시퀀스가 생성되면 식의 결과는 False입니다.  
  
-   테스트 식의 결과로 단일 부울 값이 생성되면 이 값이 식의 결과입니다.  
  
-   테스트 식의 결과로 하나 이상의 노드 시퀀스가 생성되면 식의 결과는 True입니다.  
  
-   위의 경우 중 하나에 해당하지 않으면 정적 오류가 발생합니다.  
  
 논리적 **하 고** 하 고 **또는** 연산자는 표준 논리적 의미 체계가 있는 식의 결과 부울 값에 적용 됩니다.  
  
 다음 쿼리는 제품 카탈로그에서 검색 전면 각도 크기가 작은 사진 인 합니다 <`Picture`>는 특정 제품 모델에 대 한 요소입니다. 각 제품 설명 문서에 대해 카탈로그에 크기 및 각도와 같은 다른 특성을 가진 하나 이상의 제품 사진을 저장할 수 있습니다.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $F in /PD:ProductDescription/PD:Picture[PD:Size="small"   
                                                 and PD:Angle="front"]  
     return   
         $F   
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 다음은 결과입니다.  
  
```  
<PD:Picture   
  xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  <PD:Angle>front</PD:Angle>  
  <PD:Size>small</PD:Size>  
  <PD:ProductPhotoID>31</PD:ProductPhotoID>  
</PD:Picture>  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [XQuery 식](../xquery/xquery-expressions.md)  
  
  
