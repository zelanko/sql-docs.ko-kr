---
title: 조건 식 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f593455269b8c005a3b4d3725f4360db77ea48f2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68039011"
---
# <a name="conditional-expressions-xquery"></a>조건 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery는 다음과 **같은 조건문을** 지원 합니다.  
  
```  
if (<expression1>)  
then  
  <expression2>  
else  
  <expression3>  
```  
  
 `expression1`의 유효한 부울 값에 따라 `expression2`나 `expression3`이 계산됩니다. 예를 들면 다음과 같습니다.  
  
-   테스트 식 `expression1`이 빈 시퀀스가 될 경우 결과는 False입니다.  
  
-   테스트 식 `expression1`이 단순한 부울 값이 될 경우 이 값은 식의 결과입니다.  
  
-   테스트 식 `expression1`이 하나 또는 여러 노드의 시퀀스가 될 경우 식의 결과는 True입니다.  
  
-   위의 경우 중 하나에 해당하지 않으면 정적 오류가 발생합니다.  
  
 다음 사항도 유의해야 합니다.  
  
-   테스트 식은 괄호로 묶어야 합니다.  
  
-   **Else** 식이 필요 합니다. 필요 없으면 이 항목의 예에 나오는 대로 " ( ) "을 반환할 수 있습니다.  
  
 예를 들어 다음 쿼리는 **xml** 유형 변수에 대해 지정 됩니다. **If** 조건은 [sql: variable () 함수](../xquery/xquery-extension-functions-sql-variable.md) 확장 함수를@v사용 하 여 XQuery 식 내에서 sql 변수 ()의 값을 테스트 합니다. 변수 값이 "FirstName" 이면 <`FirstName`> 요소를 반환 합니다. 그렇지 않으면 <`LastName`> 요소를 반환 합니다.  
  
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
  
 다음 쿼리는 특정 제품 모델의 제품 카탈로그 설명에서 처음 두 개의 기능 설명을 검색합니다. 문서에 더 많은 기능이 있는 경우 빈 콘텐츠가 포함 된 <`there-is-more`> 요소를 추가 합니다.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  
 이전 쿼리에서 **if** 식의 조건은 <`Features`>에 자식 요소가 두 개 이상 있는지 여부를 확인 합니다. 3개 이상일 경우 결과에 `\<there-is-more/>` 요소를 반환합니다.  
  
 다음은 결과입니다.  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  \<p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p1:WarrantyPeriod>3 years\</p1:WarrantyPeriod>  
    \<p1:Description>parts and labor\</p1:Description>  
  \</p1:Warranty>  
  \<p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p2:NoOfYears>10 years\</p2:NoOfYears>  
    \<p2:Description>maintenance contract available through your dealer or any AdventureWorks retail store.\</p2:Description>  
  \</p2:Maintenance>  
  \<there-is-more />  
</Product>  
```  
  
 다음 쿼리에서는 작업 센터 위치에서 `Location` 설정 시간을 지정 하지 않은 경우 locationid 특성이 있는 <> 요소가 반환 됩니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
 다음 예제와 같이 **if** 절 없이이 쿼리를 작성할 수 있습니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in //AWMI:root/AWMI:Location[not(@SetupHours)]   
        return  
          <Location>  
             { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="see-also"></a>참고 항목  
 [XQuery 식](../xquery/xquery-expressions.md)  
  
  
