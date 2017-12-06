---
title: "비교 식 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- node comparison operators [XQuery]
- comparison expressions [XQuery]
- node order comparison operators [XQuery]
- expressions [XQuery], comparison
- comparison operators [XQuery]
- value comparison operators
ms.assetid: dc671348-306f-48ef-9e6e-81fc3c7260a6
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 09bf123f7c3b1175c004c4d4a173c667d505aad1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="comparison-expressions-xquery"></a>비교 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery는 다음 유형의 비교 연산자를 제공합니다.  
  
-   일반 비교 연산자  
  
-   값 비교 연산자  
  
-   노드 비교 연산자  
  
-   노드 순서 비교 연산자  
  
## <a name="general-comparison-operators"></a>일반 비교 연산자  
 일반 비교 연산자는 원자 값, 시퀀스 또는 이 둘의 조합을 비교하는 데 사용할 수 있습니다.  
  
 일반 연산자는 다음 표에 정의되어 있습니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|=|같음|  
|!=|같지 않음|  
|\<|보다 작음|  
|>|보다 큼|  
|\<=|작거나 같음|  
|>=|크거나 같음|  
  
 일반 비교 연산자를 사용하여 두 시퀀스를 비교할 때 True와 첫 번째 시퀀스에 있는 값을 비교하는 두 번째 시퀀스에 값이 있으면 전체 결과는 True이고 그렇지 않으면 False입니다. 예를 들어 (1, 2, 3) = (3, 4)는 값 3이 두 시퀀스에 모두 나타나므로 True입니다.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3) = (3,4)')    
```  
  
 비교를 통해 값이 비교 가능한 유형인지 예측할 수 있습니다. 특히 이러한 값은 정적으로 확인됩니다. 숫자 비교의 경우 숫자 유형 승격이 발생할 수 있습니다. 예를 들어 10진수 값 10을 double 값 1e1과 비교하면 10진수 값이 double로 변경됩니다. 이렇게 하면 double 비교가 정확하지 않을 수 있으므로_ 부정확한 결과가 만들어질 수 있습니다.  
  
 값 중 하나가 형식화되지 않은 경우 다른 값의 유형으로 캐스팅됩니다. 다음 예에서 값 7은 정수로 처리됩니다. 비교되기 전에 형식화되지 않은 값 /a[1]은 정수로 변환됩니다. 정수 비교는 True를 반환합니다.  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < 7')  
```  
  
 반대로 형식화되지 않은 값을 문자열이나 형식화되지 않은 다른 값과 비교하면 xs:string으로 캐스팅됩니다. 다음 쿼리에서는 문자열 6과 문자열 "17"을 비교합니다. 다음 쿼리는 문자열 비교이므로 False를 반환합니다.  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < "17"')  
```  
  
 다음 쿼리는 AdventureWorks 예제 데이터베이스에 제공된 제품 카탈로그의 제품 모델에 대한 크기가 작은 사진을 반환합니다. 이 쿼리는 `PD:ProductDescription/PD:Picture/PD:Size`에서 반환되는 원자 값 시퀀스와 단일 시퀀스 "small"을 비교합니다. 경우 비교는 True를 반환 된 < 그림\> 요소입니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('         
    for $P in /PD:ProductDescription/PD:Picture[PD:Size = "small"]         
    return $P') as Result         
FROM   Production.ProductModel         
WHERE  ProductModelID=19         
```  
  
 다음 쿼리는 일련의 전화 번호에 비교 < 번호\> 요소를 사용 하는 문자열 리터럴 "112-111-1111"입니다. 이 쿼리는 AdditionalContactInfo 열에 있는 전화 번호 요소의 시퀀스를 비교하여 특정 고객에 대한 특정 전화 번호가 문서에 있는지 확인합니다.  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.value('         
   /aci:AdditionalContactInfo//act:telephoneNumber/act:number = "112-111-1111"', 'nvarchar(10)') as Result         
FROM Person.Contact         
WHERE ContactID=1         
```  
  
 쿼리에서 True를 반환합니다. 이는 번호가 문서에 있다는 의미입니다. 다음 쿼리는 위의 쿼리를 약간 수정한 버전입니다. 이 쿼리에서는 문서에서 검색한 전화 번호 값이 두 개의 전화 번호 값 시퀀스와 비교됩니다. 비교가 True 인 경우는 < 번호\> 요소가 반환 됩니다.  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('         
  if (/aci:AdditionalContactInfo//act:telephoneNumber/act:number = ("222-222-2222","112-111-1111"))         
  then          
     /aci:AdditionalContactInfo//act:telephoneNumber/act:number         
  else         
    ()') as Result         
FROM Person.Contact         
WHERE ContactID=1  
  
```  
  
 다음은 결과입니다.  
  
```  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    112-111-1111  
\</act:number>   
```  
  
## <a name="value-comparison-operators"></a>값 비교 연산자  
 값 비교 연산자는 원자 값을 비교하는 데 사용됩니다. 쿼리에 값 비교 연산자 대신 일반 비교 연산자를 사용할 수 있습니다.  
  
 값 비교 연산자는 다음 표에 정의되어 있습니다.  
  
|연산자|Description|  
|--------------|-----------------|  
|eq|같음|  
|ne|같지 않음|  
|lt|보다 작음|  
|gt|보다 큼|  
|le|작거나 같음|  
|ge|크거나 같음|  
  
 두 값을 비교하여 선택한 연산자와 같으면 식은 True를 반환하고 그렇지 않으면 False를 반환합니다. 한 값이 빈 시퀀스이면 식 결과는 False입니다.  
  
 이러한 연산자는 단일 원자 값에서만 사용할 수 있습니다. 즉, 시퀀스를 피연산자 중 하나로 지정할 수 없습니다.  
  
 예를 들어 다음 쿼리 검색 \<그림 > 요소는 그림 크기가 제품 모델에 대 한 "작은:  
  
```  
SELECT CatalogDescription.query('         
              declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";         
              for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]         
              return         
                    $P         
             ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=19         
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   `declare namespace`는 다음에 쿼리에서 사용되는 네임스페이스 접두사를 정의합니다.  
  
-   \<크기 > 요소 값의 지정 된 원자 값인 "small"과 비교 됩니다.  
  
-   값 연산자는 원자 값 에서만 작동 하기 때문에 사용자에 게 유의 **data ()** 함수는 암시적으로 노드 값을 검색 하는 데 사용 됩니다. 즉 `data($P/PD:Size) eq "small"`은 같은 결과를 생성합니다.  
  
 다음은 결과입니다.  
  
```  
\<PD:Picture   
  xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  \<PD:Angle>front\</PD:Angle>  
  \<PD:Size>small\</PD:Size>  
  \<PD:ProductPhotoID>31\</PD:ProductPhotoID>  
\</PD:Picture>  
```  
  
 값 비교에 대한 형식 승격 규칙은 일반 비교의 경우와 동일합니다. 또한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 일반 비교 중에 형식화되지 않은 값에 대해 사용하는 캐스트 규칙을 값 비교 중에도 사용합니다. 이와는 반대로 XQuery 사양의 규칙은 값 비교 중에 형식화되지 않은 값을 항상 xs:string으로 캐스팅합니다.  
  
## <a name="node-comparison-operator"></a>노드 비교 연산자  
 노드 비교 연산자 **은**, 노드 형식에만 적용 됩니다. 이 연산자가 반환하는 결과는 피연산자로 전달된 두 노드가 원본 문서의 같은 노드를 나타내는지 여부를 나타냅니다. 이 연산자는 두 피연산자가 같은 노드이면 True를 반환하고 그렇지 않으면 False를 반환합니다.  
  
 다음 쿼리는 업무 센터 위치 10이 특정 제품 모델의 제조 프로세스에서 첫 번째인지 여부를 확인합니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions' AS AWMI)  
  
SELECT ProductModelID, Instructions.query('         
    if (  (//AWMI:root/AWMI:Location[@LocationID=10])[1]         
          is          
          (//AWMI:root/AWMI:Location[1])[1] )          
    then         
          <Result>equal</Result>         
    else         
          <Result>Not-equal</Result>         
         ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=7           
```  
  
 다음은 결과입니다.  
  
```  
ProductModelID       Result          
-------------- --------------------------  
7              <Result>equal</Result>      
```  
  
## <a name="node-order-comparison-operators"></a>노드 순서 비교 연산자  
 노드 순서 비교 연산자는 문서에서 연산자의 위치를 기준으로 노드 쌍을 비교합니다.  
  
 이러한 연산자는 문서 순서를 기준으로 생성된 비교 연산자입니다.  
  
-   `<<`: **Operand 1** 앞에 야 **operand 2** 문서 순서로 합니다.  
  
-   `>>`: **Operand 1** 따라 **operand 2** 문서 순서로 합니다.  
  
 다음 쿼리는 제품 카탈로그 설명에 있으면 True를 반환 합니다는 \<보증 > 요소 앞에 나타나는 \<유지 관리 > 특정 제품에 대 한 문서 순서입니다.  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS WM)  
  
SELECT CatalogDescription.value('  
     (/PD:ProductDescription/PD:Features/WM:Warranty)[1] <<   
           (/PD:ProductDescription/PD:Features/WM:Maintenance)[1]', 'nvarchar(10)') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **value ()** 의 메서드는 **xml**데이터 형식은 쿼리에서 사용 됩니다.  
  
-   쿼리의 부울 결과 변환 **nvarchar (10)** 반환 합니다.  
  
-   쿼리에서 True를 반환합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [형식 시스템 &#40; XQuery &#41;](../xquery/type-system-xquery.md)   
 [XQuery 식](../xquery/xquery-expressions.md)  
  
  
