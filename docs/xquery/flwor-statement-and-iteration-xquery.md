---
title: FLWOR 문 및 반복 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- return clause
- FLWOR statement
- effective Boolean value [XQuery]
- multiple variable binding
- order by clause [XQuery]
- for clause [XQuery]
- where clause [XQuery]
- iterations [XQuery]
- XQuery, FLWOR statement
- EBV
ms.assetid: d7cd0ec9-334a-4564-bda9-83487b6865cb
caps.latest.revision: 44
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8e0cfb089688407dd35ce1958785276b8f647d26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="flwor-statement-and-iteration-xquery"></a>FLWOR 문 및 반복(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery는 FLWOR 반복 구문을 정의합니다. FLWOR는 `for`, `let`, `where`, `order by` 및 `return`의 머리 글자어입니다.  
  
 FLWOR 문은 다음과 같은 부분으로 구성됩니다.  
  
-   하나 이상의 반복기 변수를 입력 시퀀스로 바인딩하는 하나 이상의 FOR 절  
  
     입력 시퀀스는 XPath 식과 같은 다른 XQuery 식이 될 수 있으며 노드 시퀀스나 원자성 값의 시퀀스 중 하나입니다. 원자성 값 시퀀스는 리터럴이나 생성자 함수를 사용하여 생성할 수 있습니다. 생성되는 XML 노드는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 입력 시퀀스로 허용되지 않습니다.  
  
-   `let` 절(옵션) 이 절은 특정 반복에 대해 지정된 변수에 값을 할당합니다. 할당된 식은 XPath 식과 같은 XQuery 식일 수 있으며 노드 시퀀스나 원자성 값 시퀀스를 반환할 수 있습니다. 원자성 값 시퀀스는 리터럴이나 생성자 함수를 사용하여 생성할 수 있습니다. 생성되는 XML 노드는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 입력 시퀀스로 허용되지 않습니다.  
  
-   반복기 변수. 이 변수는 `as` 키워드를 사용하여 옵션의 형식 어설션을 가질 수 있습니다.  
  
-   `where` 절(옵션) 이 절은 반복에 필터 조건자를 적용합니다.  
  
-   `order by` 절(옵션)  
  
-   `return` 식. `return` 절의 식은 FLWOR 문의 결과를 구성합니다.  
  
 예를 들어 다음 쿼리는 첫 번째 제조 위치의 <`Step`> 요소를 통해 반복되는데 <`Step`>노드의 문자열 값을 반환합니다.  
  
```  
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $step in /ManuInstructions/Location[1]/Step  
   return string($step)  
')  
```  
  
 다음은 결과입니다.  
  
```  
Manu step 1 at Loc 1 Manu step 2 at Loc 1 Manu step 3 at Loc 1  
```  
  
 다음 쿼리는 ProductModel 테이블의 형식화된 xml 열인 Instructions 열에 대해 지정된다는 점을 제외하고 이전 쿼리와 유사합니다. 쿼리는 특정 제품에 대한 첫 번째 작업 센터 위치의 모든 제조 단계인 <`step`> 요소를 통해 반복됩니다.  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in //AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   `$Step`은 반복기 변수입니다.  
  
-   [경로 식](../xquery/path-expressions-xquery.md), `//AWMI:root/AWMI:Location[1]/AWMI:step`, 입력된 시퀀스를 생성 합니다. 이 시퀀스는 첫 번째 <`Location`> 요소 노드의 <`step`> 요소 노드 자식에 대한 시퀀스입니다.  
  
-   조건부 절 `where`(옵션)는 사용되지 않습니다.  
  
-   `return` 식은 <`step`> 요소의 문자열 값을 반환합니다.  
  
 [string 함수 (XQuery)](../xquery/data-accessor-functions-string-xquery.md) 의 문자열 값을 검색 하는 데 사용 되는 <`step`> 노드.  
  
 다음은 결과의 일부입니다.  
  
```  
Insert aluminum sheet MS-2341 into the T-85A framing tool.   
Attach Trim Jig TJ-26 to the upper and lower right corners of   
the aluminum sheet. ....         
```  
  
 다음은 허용되는 그 밖의 다른 입력 시퀀스의 예입니다.  
  
```  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in (1, 2, 3)  
  return $a')  
-- result = 1 2 3   
  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in   
   for $b in (1, 2, 3)  
      return $b  
return $a')  
-- result = 1 2 3  
  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('  
  for $a in (xs:string( "test"), xs:double( "12" ), data(/ROOT/a ))  
  return $a')  
-- result test 12 111  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 다른 유형의 시퀀스는 허용되지 않습니다. 특히 원자성 값과 노드가 혼합된 시퀀스는 허용되지 않습니다.  
  
 반복이과 함께 자주 사용 되는 [XML 생성](../xquery/xml-construction-xquery.md) 다음 쿼리에서와 같이 XML 변환에서 구문 형식을 지정 합니다.  
  
 AdventureWorks 샘플 데이터베이스에서에 저장 된 제조 지침의 **지침** 의 열은 **Production.ProductModel** 테이블이 다음과 같은 형식:  
  
```  
<Location LocationID="10" LaborHours="1.2"   
            SetupHours=".2" MachineHours=".1">  
  <step>describes 1st manu step</step>  
   <step>describes 2nd manu step</step>  
   ...  
</Location>  
...  
```  
  
 다음 쿼리는 작업 센터 위치 특성이 자식 요소로 반환되고 <`Location`> 요소가 있는 새 XML을 생성합니다.  
  
```  
<Location>  
   <LocationID>10</LocationID>  
   <LaborHours>1.2</LaborHours>  
   <SetupHours>.2</SteupHours>  
   <MachineHours>.1</MachineHours>  
</Location>  
...  
```  
  
 다음은 쿼리입니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in /AWMI:root/AWMI:Location  
        return  
          <Location>  
            <LocationID> { data($WC/@LocationID) } </LocationID>  
            <LaborHours>   { data($WC/@LaborHours) }   </LaborHours>  
            <SetupHours>   { data($WC/@SetupHours) }   </SetupHours>  
            <MachineHours> { data($WC/@MachineHours) } </MachineHours>  
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   FLWOR 문은 특정 제품에 대한 <`Location`> 요소의 시퀀스를 검색합니다.  
  
-   [데이터 함수 (XQuery)](../xquery/data-accessor-functions-data-xquery.md) 특성으로 대신 텍스트 노드로 결과 XML에 추가할 수는 각 특성의 값을 추출 하는 데 사용 됩니다.  
  
-   RETURN 절의 식은 원하는 XML을 생성합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<Location>  
  <LocationID>10</LocationID>  
  <LaborHours>2.5</LaborHours>  
  <SetupHours>0.5</SetupHours>  
  <MachineHours>3</MachineHours>  
</Location>  
<Location>  
   ...  
<Location>  
...  
```  
  
## <a name="using-the-let-clause"></a>let 절 사용  
 `let` 절을 사용하여 변수를 통해 참조할 수 있는 반복 식의 이름을 지정할 수 있습니다. 쿼리에서 변수가 참조될 때마다 `let` 변수에 할당된 식이 쿼리에 삽입됩니다. 즉, 문이 식이 참조될 때마다 실행됩니다.  
  
 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스의 제조 지침에는 필요한 도구와 이러한 도구가 사용되는 위치에 대한 정보가 포함됩니다. 다음 쿼리에서는 `let` 절을 사용하여 제품 모델을 빌드하는 데 필요한 도구와 각 도구가 필요한 위치를 나열합니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $T in //AWMI:tool  
            let $L := //AWMI:Location[.//AWMI:tool[.=data($T)]]  
        return  
          <tool desc="{data($T)}" Locations="{data($L/@LocationID)}"/>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="using-the-where-clause"></a>Where 절 사용  
 `where` 절을 사용하여 반복 결과를 필터링할 수 있습니다. 다음 예에서 이를 확인할 수 있습니다.  
  
 자전거를 제조할 경우 제조 과정은 여러 위치의 작업 센터를 통해 진행됩니다. 각 작업 센터 위치는 제조 단계 시퀀스를 정의합니다. 다음 쿼리는 자전거 모델을 제조하고 제조 단계가 3개 미만인 작업 센터 위치만 검색합니다. 즉 이러한 작업 센터 위치에는 <`step`> 요소가 3개 미만입니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location  
      where count($WC/AWMI:step) < 3  
      return  
          <Location >  
           { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하십시오.  
  
-   `where` 키워드를 사용 하는 **count ()** 의 수를 계산 하는 함수 <`step`> 자식 요소에 각 작업 센터 위치입니다.  
  
-   `return` 식은 반복 결과로부터 원하는 XML을 생성합니다.  
  
 다음은 결과입니다.  
  
```  
<Location LocationID="30"/>   
```  
  
 `where` 절에 있는 식의 결과는 지정된 순서대로 다음 규칙에 따라 부울 값으로 변환됩니다. 이러한 규칙은 정수가 허용되지 않는다는 점을 제외하고 경로 식의 조건자에 대한 규칙과 동일합니다.  
  
1.  `where` 식이 빈 시퀀스를 반환하는 경우 유효한 부울 값은 False입니다.  
  
2.  `where` 식이 하나의 단순 부울 형식 값을 반환하는 경우 이 값은 유효한 부울 값입니다.  
  
3.  `where` 식이 하나 이상의 노드가 포함된 시퀀스를 반환하는 경우 유효한 부울 값은 True입니다.  
  
4.  그 밖의 경우에는 정적 오류가 발생합니다.  
  
## <a name="multiple-variable-binding-in-flwor"></a>FLWOR의 복수 변수 바인딩  
 여러 개의 변수를 입력 시퀀스에 바인딩하는 FLWOR 식을 하나만 사용할 수 있습니다. 다음 예에서는 형식화되지 않은 xml 변수에 대해 쿼리가 지정됩니다. FLOWR 식은 각 <`Location`> 요소에 있는 첫 번째<`Step`> 요소 자식을 반환합니다.  
  
```  
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $Loc in /ManuInstructions/Location,  
       $FirstStep in $Loc/Step[1]  
   return   
       string($FirstStep)  
')  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   `for` 식 정의 `$Loc` 및 $`FirstStep` 변수입니다.  
  
-   `two`의 값이 `/ManuInstructions/Location`의 값에 종속되는 경우 `$FirstStep in $Loc/Step[1]` 식, `$FirstStep`과 `$Loc`은 상호 관련됩니다.  
  
-   `$Loc`와 관련된 식은 <`Location`> 요소의 시퀀스를 생성합니다. 각 <`Location`> 요소마다 `$FirstStep`은 하나의 <`Step`> 요소, 즉 단일 시퀀스를 생성합니다.  
  
-   `$Loc`은 `$FirstStep` 변수와 관련된 식에서 지정됩니다.  
  
 다음은 결과입니다.  
  
```  
Manu step 1 at Loc 1   
Manu step 1 at Loc 2  
```  
  
 다음 쿼리는 형식화 된 Instructions 열에 대해 지정 된다는 점을 제외 하 고 마찬가지로 **xml** 열에서의 **ProductModel** 테이블입니다. [XML 생성 (XQuery)](../xquery/xml-construction-xquery.md) 원하는 XML을 생성 하는 데 사용 됩니다.  
  
```  
SELECT Instructions.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /root/Location,  
            $S  in $WC/step  
      return  
          <Step LocationID= "{$WC/@LocationID }" >  
            { $S/node() }  
          </Step>  
') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하십시오.  
  
-   `for` 절은 두 개의 변수 `$WC`와 `$S`를 정의합니다. `$WC`와 관련된 식은 자전거 제품 모델을 제조하는 작업 센터 위치의 시퀀스를 생성합니다. `$S` 변수에 할당되는 경로 식은 `$WC`에 있는 각 작업 센터 위치 시퀀스에 대한 단계의 시퀀스를 생성합니다.  
  
-   Return 문을 XML을 생성 한 <`Step`> 제조 단계가 포함 된 요소 및 **LocationID** 그 특성으로 합니다.  
  
-   **기본 요소 네임 스페이스 선언** 결과 XML의 모든 네임 스페이스 선언이 최상위 요소에 나타나도록 XQuery 프롤로그에 사용 됩니다. 따라서 결과가 더 읽기 쉬워집니다. 기본 네임 스페이스에 대 한 자세한 내용은 참조 [XQuery의 네임 스페이스 처리](../xquery/handling-namespaces-in-xquery.md)합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<Step xmlns=  
    "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
  LocationID="10">  
     Insert <material>aluminum sheet MS-2341</material> into the <tool>T-   
     85A framing tool</tool>.   
</Step>  
...  
<Step xmlns=  
      "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
    LocationID="20">  
        Assemble all frame components following blueprint   
        <blueprint>1299</blueprint>.  
</Step>  
...  
```  
  
## <a name="using-the-order-by-clause"></a>order by 절 사용  
 XQuery에서는 FLWOR 식의 `order by` 절을 사용하여 정렬이 수행됩니다. 정렬 식에 전달 되는 `order by` 절 형식이 적합 되는 값을 반환 해야 합니다는 **gt** 연산자입니다. 각 정렬 식의 결과는 한 항목의 단일 시퀀스여야 합니다. 기본적으로 정렬은 오름차순으로 수행됩니다. 각 정렬 식에 대해 선택적으로 오름차순이나 내림차순을 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 XQuery를 구현하여 수행된 문자열 값을 정렬하는 비교는 항상 이진 유니코드 코드 포인트 데이터 정렬을 사용하여 수행됩니다.  
  
 다음 쿼리는 AdditionalContactInfo 열에서 특정 고객에 대한 모든 전화 번호를 검색합니다. 결과는 전화 번호를 기준으로 정렬됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AdditionalContactInfo.query('  
   declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 [원자화 (XQuery)](../xquery/atomization-xquery.md) 의 원자성 값을 검색 하는 프로세스는 <`number`> 요소에 전달 하기 전에 `order by`합니다. 사용 하 여 식을 작성할 수는 **data ()** 함수가 있지만 필요 하지 않습니다.  
  
```  
order by data($a/act:number[1]) descending  
```  
  
 다음은 결과입니다.  
  
```  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
```  
  
 쿼리 프롤로그에서 네임스페이스를 선언하는 대신 WITH XMLNAMESPACES를 사용하여 선언할 수 있습니다.  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo'  AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 특성 값을 기준으로 정렬할 수도 있습니다. 예를 들어 다음 쿼리는 새로 만든 <`Location`> 요소를 검색하는데 이 요소에는 LaborHours 특성을 기준으로 내림차순으로 LocationID 및 LaborHours 특성이 정렬되어 있습니다. 따라서 노동 시간이 가장 많은 작업 센터 위치가 가장 먼저 반환됩니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location   
order by $WC/@LaborHours descending  
        return  
          <Location>  
             { $WC/@LocationID }   
             { $WC/@LaborHours }   
          </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 다음은 결과입니다.  
  
```  
<Location LocationID="60" LaborHours="4"/>  
<Location LocationID="50" LaborHours="3"/>  
<Location LocationID="10" LaborHours="2.5"/>  
<Location LocationID="20" LaborHours="1.75"/>  
<Location LocationID="30" LaborHours="1"/>  
<Location LocationID="45" LaborHours=".5"/>  
```  
  
 다음 쿼리에서 결과는 요소 이름을 기준으로 정렬됩니다. 쿼리는 제품 카탈로그에서 특정 제품의 사양을 검색합니다. 사양은 <`Specifications`> 요소의 자식입니다.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace  
 pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $a in /pd:ProductDescription/pd:Specifications/*   
     order by local-name($a)  
      return $a  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19;  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   `/p1:ProductDescription/p1:Specifications/*` 식은 <`Specifications`>의 요소 자식을 반환합니다.  
  
-   `order by (local-name($a))` 식은 요소 이름의 로컬 부분을 기준으로 시퀀스를 정렬합니다.  
  
 다음은 결과입니다.  
  
```  
<Color>Available in most colors</Color>  
<Material>Almuminum Alloy</Material>  
<ProductLine>Mountain bike</ProductLine>  
<RiderExperience>Advanced to Professional riders</RiderExperience>  
<Style>Unisex</Style>    
```  
  
 순서 지정 식에서 빈 결과를 반환하는 노드는 다음 예에서 볼 수 있듯이 시퀀스의 시작 부분에 정렬됩니다.  
  
```  
declare @x xml  
set @x='<root>  
  <Person Name="A" />  
  <Person />  
  <Person Name="B" />  
</root>  
'  
select @x.query('  
  for $person in //Person  
  order by $person/@Name  
  return   $person  
')  
```  
  
 다음은 결과입니다.  
  
```  
<Person />  
<Person Name="A" />  
<Person Name="B" />  
```  
  
 다음 예에서 볼 수 있듯이 여러 정렬 기준을 지정할 수 있습니다. 이 예의 쿼리는 <`Employee`> 요소를 먼저 Title 특성 값을 기준으로 정렬한 다음 Administrator 특성 값을 기준으로 정렬합니다.  
  
```  
declare @x xml  
set @x='<root>  
  <Employee ID="10" Title="Teacher"        Gender="M" />  
  <Employee ID="15" Title="Teacher"  Gender="F" />  
  <Employee ID="5" Title="Teacher"         Gender="M" />  
  <Employee ID="11" Title="Teacher"        Gender="F" />  
  <Employee ID="8" Title="Administrator"   Gender="M" />  
  <Employee ID="4" Title="Administrator"   Gender="F" />  
  <Employee ID="3" Title="Teacher"         Gender="F" />  
  <Employee ID="125" Title="Administrator" Gender="F" /></root>'  
SELECT @x.query('for $e in /root/Employee  
order by $e/@Title ascending, $e/@Gender descending  
  
  return  
     $e  
')  
```  
  
 다음은 결과입니다.  
  
```  
<Employee ID="8" Title="Administrator" Gender="M" />  
<Employee ID="4" Title="Administrator" Gender="F" />  
<Employee ID="125" Title="Administrator" Gender="F" />  
<Employee ID="10" Title="Teacher" Gender="M" />  
<Employee ID="5" Title="Teacher" Gender="M" />  
<Employee ID="11" Title="Teacher" Gender="F" />  
<Employee ID="15" Title="Teacher" Gender="F" />  
<Employee ID="3" Title="Teacher" Gender="F" />  
```  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   정렬 식은 같은 유형으로 형식화되어야 합니다. 이 제한은 정적으로 확인됩니다.  
  
-   빈 시퀀스를 정렬하는 작업은 제어할 수 없습니다.  
  
-   `order by`에서는 빈 최소값, 빈 최대값 및 데이터 정렬 키워드가 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XQuery 식](../xquery/xquery-expressions.md)  
  
  
