---
title: 계층 구조와 관련 된 XQueries | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
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
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9344936bfe684061ea6683870ffd47b43e261810
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="xqueries-involving-hierarchy"></a>계층 포함 XQuery
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  대부분 **xml** 유형 열에는 **AdventureWorks** 데이터베이스는 반 구조화 된 문서입니다. 따라서 각 행에 저장된 문서는 다르게 보일 수 있습니다. 이 항목의 쿼리 예제에서는 이러한 여러 문서로부터 정보를 추출하는 방법을 보여 줍니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>1. 제조 지침 문서에서 작업 센터 위치와 해당 위치의 첫 번째 제조 단계 검색  
 쿼리는 제품 모델 7에 대해 포함 된 XML을 생성은 <`ManuInstr`> 요소와 **ProductModelID** 및 **ProductModelName** 특성 및 하나 이상의 <`Location`> 자식 요소입니다.  
  
 각 <`Location`> 요소에는 자체 특성 집합과 하나의 <`step`> 자식 요소가 있습니다. 이 <`step`> 자식 요소는 작업 센터 위치의 첫 번째 제조 단계입니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   \<ManuInstr  ProdModelID = "{sql:column("Production.ProductModel.ProductModelID") }"   
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
            {   
              for $wc in //AWMI:root/AWMI:Location  
              return  
                <Location>  
                 {$wc/@* }  
                 <step1> { string( ($wc//AWMI:step)[1] ) } </step1>  
                </Location>  
            }  
          </ManuInstr>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **네임 스페이스** 키워드는 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 네임 스페이스 접두사를 정의 합니다. 이 접두사는 나중에 쿼리 본문에서 사용됩니다.  
  
-   컨텍스트 변환 토큰인 {)와 (}는 XML 생성의 쿼리를 쿼리 평가로 변환하는 데 사용됩니다.  
  
-   **: column ()** 생성 되는 XML의 관계형 값을 포함 하는 데 사용 됩니다.  
  
-   <`Location`> 요소를 생성할 때 $wc/@*는 모든 작업 센터 위치 특성을 검색합니다.  
  
-   **string ()** 에서 문자열 값을 반환 하는 함수는 <`step`> 요소입니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<ManuInstr ProdModelID="7" ProductModelName="HL Touring Frame">  
   <Location LocationID="10" SetupHours="0.5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
     <step1>Insert aluminum sheet MS-2341 into the T-85A   
             framing tool.</step1>  
   </Location>  
   <Location LocationID="20" SetupHours="0.15"   
            MachineHours="2" LaborHours="1.75" LotSize="1">  
      <step1>Assemble all frame components following   
             blueprint 1299.</step1>  
   </Location>  
...  
</ManuInstr>   
```  
  
### <a name="b-find-all-telephone-numbers-in-the-additionalcontactinfo-column"></a>2. AdditionalContactInfo 열에서 모든 전화 번호 찾기  
 다음 쿼리는 <`telephoneNumber`> 요소에 대한 전체 계층을 검색하여 특정 고객 연락처의 추가 전화 번호를 검색합니다. <`telephoneNumber`> 요소는 계층의 아무 곳에나 표시될 수 있기 때문에 이 쿼리는 검색 시 하위 항목과 자체 연산자(//)를 사용합니다.  
  
```  
SELECT AdditionalContactInfo.query('  
 declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
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
  
 <`AdditionalContactInfo`>의 <`telephoneNumber`> 자식 요소와 같이 최상위 전화 번호만 검색하려면 쿼리의 FOR 식이 다음으로 변경됩니다.  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XQuery 기초](../xquery/xquery-basics.md)   
 [XML 생성 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
