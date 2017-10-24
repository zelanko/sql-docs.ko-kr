---
title: "식 (XQuery) 수치화 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
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
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 483c3779e53389d34da12c974f3a13672216c9a9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="quantified-expressions-xquery"></a>정량화된 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  존재 및 범용 수량자는 두 가지 시퀀스에 적용되는 부울 연산자에 다른 의미 체계를 지정합니다. 다음 표에서는 이러한 수량자를 보여 줍니다.  
  
 *존재 수량자*  
 두 개의 시퀀스에서 사용된 비교 연산자를 기준으로 첫 번째 시퀀스의 임의 항목이 두 번째 시퀀스의 항목과 일치하면 True 값이 반환됩니다.  
  
 *범용 수량자*  
 두 개의 시퀀스에서 첫 번째 시퀀스의 모든 항목이 두 번째 시퀀스의 항목과 일치하면 True 값이 반환됩니다.  
  
 XQuery는 다음 형식의 정량화된 식을 지원합니다.  
  
```  
( some | every ) <variable> in <Expression> (,…) satisfies <Expression>  
```  
  
 쿼리에 이러한 식을 사용하여 하나 이상의 시퀀스에서 존재 또는 범용 정량화를 명시적으로 식에 적용할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 `satisfies` 절에 있는 식의 결과가 노드 시퀀스, 빈 시퀀스 또는 부울 값 중 하나여야 합니다. 식의 결과에 알맞은 부울 값이 정량화에 사용됩니다. 사용 하는 존재 정량화 **일부** satisfy 식에서 결과가 수량자로 바인딩된 값 중 하나 이상 있으면 True를 반환 합니다. 사용 하는 범용 정량화 **모든** 수량자로 바인딩된 모든 값에 대해 True 여야 합니다.  
  
 다음 검사를 쿼리 하는 예를 들어 모든 \<위치 > 요소에 LocationID 특성 여부를 확인 합니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
 LocationID의 필수 특성 이므로 \<위치 > 요소를 예상한 결과가 나타납니다.  
  
```  
<Result>All work centers have Location ID</Result>   
```  
  
 사용 하는 대신는 [query () 메서드](../t-sql/xml/query-method-xml-data-type.md)를 사용할 수 있습니다는 [value () 메서드에](../t-sql/xml/value-method-xml-data-type.md) 다음 쿼리에서와 같이 관계형 외부에 결과 반환 하려면. 모든 업무 센터 위치에 LocationID 특성이 있으면 쿼리에서 True를 반환하고 그렇지 않으면 False를 반환합니다.  
  
```  
SELECT Instructions.value('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        every $WC in  //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID',   
  'nvarchar(10)') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 다음 쿼리에서는 제품 사진 중 하나의 크기가 작은지 확인합니다. 제품 카탈로그 XML에 각 제품 사진이 다른 크기로 다양하게 저장되어 있습니다. 제품 카탈로그 XML마다 하나 이상의 작은 사진이 들어 있는지 확인할 수 있습니다. 다음 쿼리에서 이 작업을 수행합니다.  
  
```  
SELECT ProductModelID, CatalogDescription.value('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  
## <a name="see-also"></a>관련 항목:  
 [XQuery 식](../xquery/xquery-expressions.md)  
  
  

