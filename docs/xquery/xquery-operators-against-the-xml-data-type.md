---
title: xml 데이터 형식에 대한 X쿼리 연산자 | 마이크로 소프트 문서
description: xml 데이터 형식에 대해 사용할 수 있는 XQuery 연산자에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
author: rothja
ms.author: jroth
ms.openlocfilehash: d5692aa5b46d79c68165fa6f1320034fdb7e03b3
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388309"
---
# <a name="xquery-operators-against-the-xml-data-type"></a>xml 데이터 형식에 대한 XQuery 연산자
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery에는 다음 연산자가 지원됩니다.  
  
-   수치 연산자(+, -, *, div, mod)  
  
-   값 비교 연산자(eq, ne, lt, gt, le, ge)  
  
-   일반 비교연산자 (=, \<!=, \<>, =, >= )  
  
 이러한 연산자에 대한 자세한 내용은 [비교 식 &#40;XQuery&#41;](../xquery/comparison-expressions-xquery.md)  
  
## <a name="examples"></a>예  
  
### <a name="a-using-general-operators"></a>A. 일반 연산자 사용  
 다음 쿼리는 시퀀스에 적용되고 시퀀스를 비교하는 일반 연산자를 사용하는 방법을 보여 줍니다. 쿼리는 **연락처** 테이블의 **AdditionalContactInfo** 열에서 각 고객에 대 한 전화 번호의 시퀀스를 검색 합니다. 그런 다음 이 번호를 두 개의 전호 번호("111-111-1111", "222-2222")와 비교합니다.  
  
 쿼리는 비교 **=** 연산자입니다. **=** 연산자의 오른쪽에 있는 시퀀스의 각 노드는 왼쪽 시퀀스의 각 노드와 비교됩니다. 노드가 일치하면 노드 비교가 **TRUE입니다.** 그런 다음 int로 변환되고 1과 비교되어 쿼리가 고객 ID를 반환합니다.  
  
```sql
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 이전 쿼리의 작동 방식을 관찰하는 또 다른 방법이 있습니다: **AdditionalContactInfo** 열에서 검색된 각 전화 번호 값은 두 전화 번호 집합과 비교됩니다. 값이 집합에 있는 경우 각 해당 고객이 결과에 반환됩니다.  
  
### <a name="b-using-a-numeric-operator"></a>B. 숫자 연산자 사용  
 이 쿼리의 + 연산자는 단일 항목에 적용되기 때문에 값 연산자입니다. 예를 들어 쿼리에 의해 반환되는 로트 크기에 값 1이 추가됩니다.  
  
```sql
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
### <a name="c-using-a-value-operator"></a>C. 값 연산자 사용  
 다음 쿼리는 그림 `Picture` 크기가 "작음"인 제품 모델의 <> 요소를 검색합니다.  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 **eq** 연산자의 피연산자는 모두 원자값이기 때문에 값 연산자가 쿼리에 사용됩니다. 일반 비교 연산자 ()를 **=** 사용하여 동일한 쿼리를 작성할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [SQL 서버&#41;&#40;XML 데이터](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
