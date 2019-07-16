---
title: 계층 구조와 관련 된 XQueries | Microsoft Docs
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
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
author: rothja
ms.author: jroth
ms.openlocfilehash: 8aa762af8e08c72f7f00369219771c371ce39aac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946103"
---
# <a name="xqueries-involving-hierarchy"></a>계층 포함 XQuery
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  대부분의 **xml** 유형 열에는 **AdventureWorks** 데이터베이스는 반 구조화 된 문서입니다. 따라서 각 행에 저장된 문서는 다르게 보일 수 있습니다. 이 항목의 쿼리 예제에서는 이러한 여러 문서로부터 정보를 추출하는 방법을 보여 줍니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. 제조 지침 문서에서 작업 센터 위치와 해당 위치의 첫 번째 제조 단계 검색  
 제품 모델 7에 대해 쿼리를 포함 하는 XML을 생성 합니다 <`ManuInstr`> 요소를 사용 하 여 **ProductModelID** 하 고 **ProductModelName** 특성 및 하나 이상의 <`Location`> 자식 요소입니다.  
  
 각 <`Location`> 요소와 특성의 고유한 집합이 <`step`> 자식 요소입니다. 이 <`step`> 자식 요소는 작업 센터 위치의 첫 번째 제조 단계입니다.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
-   합니다 **네임 스페이스** 키워드는 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 네임 스페이스 접두사를 정의 합니다. 이 접두사는 나중에 쿼리 본문에서 사용됩니다.  
  
-   컨텍스트 변환 토큰인 {)와 (}는 XML 생성의 쿼리를 쿼리 평가로 변환하는 데 사용됩니다.  
  
-   합니다 **1!s!sql:column ()** 생성 되는 XML의 관계형 값을 포함 하는 데 사용 됩니다.  
  
-   생성은 <`Location`> 요소를 $wc/@* 모든 작업 센터 위치 특성을 검색 합니다.  
  
-   합니다 **string ()** 함수에서 문자열 값을 반환 합니다 <`step`> 요소입니다.  
  
 다음은 결과의 일부입니다.  
  
```xml
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
  
### <a name="b-find-all-telephone-numbers-in-the-additionalcontactinfo-column"></a>2\. AdditionalContactInfo 열에서 모든 전화 번호 찾기  
 에 대 한 전체 계층 구조를 검색 하 여 특정 고객 연락처에 대 한 추가 전화 번호를 검색 하는 다음 쿼리는 <`telephoneNumber`> 요소입니다. 때문에 <`telephoneNumber`> 요소의 아무 위치에 계층 하위 항목과 자체 연산자를 사용 하 여 쿼리 (/ /) 검색에서 합니다.  
  
```sql
SELECT AdditionalContactInfo.query('  
 declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 다음은 결과입니다.  
  
```xml
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 특히 최상위 전화 번호만 검색 하는 <`telephoneNumber`> 자식 요소 <`AdditionalContactInfo`>, 쿼리의 FOR 식이 변경  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`항목을 참조하세요.  
  
## <a name="see-also"></a>참조  
 [XQuery 기초](../xquery/xquery-basics.md)   
 [XML 생성 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
