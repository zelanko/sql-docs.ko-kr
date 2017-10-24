---
title: "XQuery 연산자에 대해 xml 데이터 형식 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70084cbe4e9fce9388e3c5c51de37412240b3d0e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="xquery-operators-against-the-xml-data-type"></a>xml 데이터 형식에 대한 XQuery 연산자
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery에는 다음 연산자가 지원됩니다.  
  
-   수치 연산자(+, -, *, div, mod)  
  
-   값 비교 연산자(eq, ne, lt, gt, le, ge)  
  
-   일반 비교 연산자 (=,! =, \<, >, \<=, > =)  
  
 이러한 연산자에 대 한 자세한 내용은 참조 하십시오. [비교 식 &#40; XQuery &#41;](../xquery/comparison-expressions-xquery.md)  
  
## <a name="examples"></a>예  
  
### <a name="a-using-general-operators"></a>1. 일반 연산자 사용  
 다음 쿼리는 시퀀스에 적용되고 시퀀스를 비교하는 일반 연산자를 사용하는 방법을 보여 줍니다. 각 고객에 대 한 일련의 전화 번호를 검색 하는 쿼리는 **AdditionalContactInfo** 의 열은 **연락처** 테이블입니다. 그런 다음 이 번호를 두 개의 전호 번호("111-111-1111", "222-2222")와 비교합니다.  
  
 쿼리에서 사용 된  **=**  비교 연산자. 오른쪽에 있는 시퀀스의 각 노드는  **=**  연산자 왼쪽에 있는 시퀀스의 각 노드를 비교 합니다. 노드가 일치 하는 경우 노드 비교는 **TRUE**합니다. 그런 다음 int로 변환되고 1과 비교되어 쿼리가 고객 ID를 반환합니다.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 이전 쿼리의 작동 방식을 관찰 하는 방법은 다른 방법이: 각 전화 번호 값에서 검색 된 **AdditionalContactInfo** 열은 두 개의 전화 번호 집합과 비교 합니다. 값이 집합에 있는 경우 각 해당 고객이 결과에 반환됩니다.  
  
### <a name="b-using-a-numeric-operator"></a>2. 숫자 연산자 사용  
 이 쿼리의 + 연산자는 단일 항목에 적용되기 때문에 값 연산자입니다. 예를 들어 쿼리에 의해 반환되는 로트 크기에 값 1이 추가됩니다.  
  
```  
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in (/AWMI:root/AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"  
                   LotSize  = "{  number($i/@LotSize) }"  
                   LotSize2 = "{ number($i/@LotSize) + 1 }"  
                   LotSize3 = "{ number($i/@LotSize) + 2 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
### <a name="c-using-a-value-operator"></a>3. 값 연산자 사용  
 다음 쿼리는 그림 크기가 "small"인 제품 모델에 대한 <`Picture`> 요소를 검색합니다.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 때문에 두 피연산자는 **eq** 연산자는 원자 값, 값이 연산자는 쿼리에서 사용 됩니다. 일반 비교 연산자를 사용 하 여 동일한 쿼리를 작성할 수 있습니다 (  **=**  ).  
  
## <a name="see-also"></a>관련 항목:  
 [Xml 데이터 형식에 대 한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  

