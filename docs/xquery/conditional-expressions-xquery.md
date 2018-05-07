---
title: 조건부 식 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, conditional expressions
- expressions [XQuery], conditional
- effective Boolean value [XQuery]
- if-then-else statement [XQuery]
- conditional expressions [XQuery]
- EBV
ms.assetid: b280dd96-c80f-4c51-bc06-a88d42174acb
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3634414fb0353c9152d317c718707c3ce26ec812
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="conditional-expressions-xquery"></a>조건 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery는 다음 조건부 지원 **if then 다른** 문:  
  
```  
if (<expression1>)  
then  
  <expression2>  
else  
  <expression3>  
```  
  
 `expression1`의 유효한 부울 값에 따라 `expression2`나 `expression3`이 계산됩니다. 예를 들어:  
  
-   테스트 식 `expression1`이 빈 시퀀스가 될 경우 결과는 False입니다.  
  
-   테스트 식 `expression1`이 단순한 부울 값이 될 경우 이 값은 식의 결과입니다.  
  
-   테스트 식 `expression1`이 하나 또는 여러 노드의 시퀀스가 될 경우 식의 결과는 True입니다.  
  
-   위의 경우 중 하나에 해당하지 않으면 정적 오류가 발생합니다.  
  
 다음 사항도 유의해야 합니다.  
  
-   테스트 식은 괄호로 묶어야 합니다.  
  
-   **다른** 식이 필요 합니다. 필요 없으면 이 항목의 예에 나오는 대로 " ( ) "을 반환할 수 있습니다.  
  
 에 대해 다음 쿼리는 지정 하는 예를 들어는 **xml** 유형 변수입니다. **경우** SQL 변수 값을 테스트 하는 조건 (@v)를 사용 하 여 XQuery 식 안에 [variable () 함수](../xquery/xquery-extension-functions-sql-variable.md) 확장 기능입니다. 변수 값이 "FirstName"이면 <`FirstName`> 요소를 반환합니다. 그렇지 않으면 <`LastName`> 요소를 반환합니다.  
  
```  
declare @x xml  
declare @v varchar(20)  
set @v='FirstName'  
set @x='  
<ROOT rootID="2">  
  <FirstName>fname</FirstName>  
  <LastName>lname</LastName>  
</ROOT>'  
SELECT @x.query('  
if ( sql:variable("@v")="FirstName" ) then  
  /ROOT/FirstName  
 else  
   /ROOT/LastName  
')  
```  
  
 다음은 결과입니다.  
  
```  
<FirstName>fname</FirstName>  
```  
  
 다음 쿼리는 특정 제품 모델의 제품 카탈로그 설명에서 처음 두 개의 기능 설명을 검색합니다. 문서에 기능이 더 있을 경우 내용이 비어 있는 <`there-is-more`> 요소를 추가합니다.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /p1:ProductDescription/@ProductModelID }  
          { /p1:ProductDescription/@ProductModelName }   
          {  
            for $f in /p1:ProductDescription/p1:Features/*[position()\<=2]  
            return  
            $f   
          }  
          {  
            if (count(/p1:ProductDescription/p1:Features/*) > 2)  
            then \<there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 이전 쿼리에서 조건에는 **경우** 두 개 이상의 자식 요소에 지 확인 하는 식을 <`Features`> 합니다. 3개 이상일 경우 결과에 `\<there-is-more/>` 요소를 반환합니다.  
  
 다음은 결과입니다.  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  \<p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p1:WarrantyPeriod>3 years\</p1:WarrantyPeriod>  
    \<p1:Description>parts and labor\</p1:Description>  
  \</p1:Warranty>  
  \<p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p2:NoOfYears>10 years\</p2:NoOfYears>  
    \<p2:Description>maintenance contract available through your dealer or any AdventureWorks retail store.\</p2:Description>  
  \</p2:Maintenance>  
  \<there-is-more />  
</Product>  
```  
  
 다음 쿼리에서는 업무 센터 위치에서 설치 시간을 지정하지 않은 경우 LocationID 특성을 가진 <`Location`> 요소가 반환됩니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in //AWMI:root/AWMI:Location  
        return  
        if ( $WC[not(@SetupHours)] )  
        then  
          <WorkCenterLocation>  
             { $WC/@LocationID }   
          </WorkCenterLocation>  
         else  
           ()  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 다음은 결과입니다.  
  
```  
<WorkCenterLocation LocationID="30" />  
<WorkCenterLocation LocationID="45" />  
<WorkCenterLocation LocationID="60" />  
```  
  
 없이이 쿼리를 작성할 수는 **경우** 다음 예제와 같이 절:  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in //AWMI:root/AWMI:Location[not(@SetupHours)]   
        return  
          <Location>  
             { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="see-also"></a>관련 항목:  
 [XQuery 식](../xquery/xquery-expressions.md)  
  
  
