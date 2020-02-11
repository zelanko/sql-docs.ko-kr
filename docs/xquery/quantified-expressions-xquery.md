---
title: 정량화 된 식 (XQuery) | Microsoft Docs
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
- universal quantifiers
- effective Boolean value [XQuery]
- quantified expressions [XQuery]
- XQuery, quantified expressions
- every expression [XQuery]
- existential quantifiers [XQuery]
- some expression [XQuery]
- EBV
- expressions [XQuery], quantifiers
ms.assetid: a3a75a6c-8f67-4923-8406-1ada546c817f
author: rothja
ms.author: jroth
ms.openlocfilehash: 1cdbff23d2158dec00b6b8d050d6a4a90341bd23
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67946370"
---
# <a name="quantified-expressions-xquery"></a>정량화된 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  존재 및 범용 수량자는 두 가지 시퀀스에 적용되는 부울 연산자에 다른 의미 체계를 지정합니다. 다음 표에서는 이러한 수량자를 보여 줍니다.  
  
 *존재 수량자*  
 두 개의 시퀀스에서 사용된 비교 연산자를 기준으로 첫 번째 시퀀스의 임의 항목이 두 번째 시퀀스의 항목과 일치하면 True 값이 반환됩니다.  
  
 *범용 수량자*  
 두 개의 시퀀스에서 첫 번째 시퀀스의 모든 항목이 두 번째 시퀀스의 항목과 일치하면 True 값이 반환됩니다.  
  
 XQuery는 다음 형식의 정량화된 식을 지원합니다.  
  
```  
( some | every ) <variable> in <Expression> (,...) satisfies <Expression>  
```  
  
 쿼리에 이러한 식을 사용하여 하나 이상의 시퀀스에서 존재 또는 범용 정량화를 명시적으로 식에 적용할 수 있습니다. 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 `satisfies` 절에 있는 식의 결과가 노드 시퀀스, 빈 시퀀스 또는 부울 값 중 하나여야 합니다. 식의 결과에 알맞은 부울 값이 정량화에 사용됩니다. **일부** 를 사용 하는 존재 정량화는 수량자에 의해 바인딩된 값 중 하나 이상이 만족 식에 true 결과가 있는 경우 true를 반환 합니다. **모든** 를 사용 하는 universal 정량화은 수량자로 바인딩된 모든 값에 대해 True 여야 합니다.  
  
 예를 들어 다음 쿼리는 모든 \<위치> 요소를 검사 하 여 locationid 특성이 있는지 여부를 확인 합니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        if (every $WC in //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID)  
        then  
             <Result>All work centers have workcenterLocation ID</Result>  
         else  
             <Result>Not all work centers have workcenterLocation ID</Result>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 LocationID는 \<Location> 요소의 필수 특성이 기 때문에 예상 결과를 수신 합니다.  
  
```  
<Result>All work centers have Location ID</Result>   
```  
  
 [Query () 메서드](../t-sql/xml/query-method-xml-data-type.md)를 사용 하는 대신 다음 쿼리와 같이 [value () 메서드](../t-sql/xml/value-method-xml-data-type.md) 를 사용 하 여 결과를 관계형 세계에 반환할 수 있습니다. 모든 업무 센터 위치에 LocationID 특성이 있으면 쿼리에서 True를 반환하고 그렇지 않으면 False를 반환합니다.  
  
```  
SELECT Instructions.value('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        every $WC in  //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID',   
  'nvarchar(10)') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 다음 쿼리에서는 제품 사진 중 하나의 크기가 작은지 확인합니다. 제품 카탈로그 XML에 각 제품 사진이 다른 크기로 다양하게 저장되어 있습니다. 제품 카탈로그 XML마다 하나 이상의 작은 사진이 들어 있는지 확인할 수 있습니다. 다음 쿼리에서 이 작업을 수행합니다.  
  
```  
SELECT ProductModelID, CatalogDescription.value('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     some $F in /PD:ProductDescription/PD:Picture  
        satisfies $F/PD:Size="small"', 'nvarchar(20)') as SmallPicturesStored  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 다음은 결과의 일부입니다.  
  
```  
ProductModelID SmallPicturesStored   
-------------- --------------------  
19             true        
```  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   정량화된 식의 변수를 바인딩할 때는 유형 어설션이 지원되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XQuery 식](../xquery/xquery-expressions.md)  
  
  
