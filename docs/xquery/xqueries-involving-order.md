---
title: Order를 포함 하는 XQueries | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- XQuery, sequence
- ordered expressions [XQuery]
ms.assetid: 4f1266c5-93d7-402d-94ed-43f69494c04b
author: rothja
ms.author: jroth
ms.openlocfilehash: 4fc30086978e26f53f7a4fdbab8a731ac2334181
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946119"
---
# <a name="xqueries-involving-order"></a>정렬 포함 XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  관계형 데이터베이스에는 시퀀스 개념이 없습니다. 예를 들어 "데이터베이스에서 첫 번째 고객 가져오기"와 같은 요청은 수행할 수 없습니다. 그러나 XML 문서를 쿼리하고 첫 번째 \<Customer> 요소를 검색할 수 있습니다. 그런 다음에는 항상 같은 고객을 검색할 수 있습니다.  
  
 이 항목에서는 문서에 노드가 표시되는 시퀀스에 기반한 쿼리에 대해 설명합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-retrieve-manufacturing-steps-at-the-second-work-center-location-for-a-product"></a>A. 제품에 대한 두 번째 작업 센터 위치에서 제조 단계 검색  
 특정 제품 모델에 대해 다음 쿼리는 두 번째 작업 센터 위치에서 제조 프로세스에 있는 작업 센터 위치의 시퀀스에 따라 제조 단계를 검색합니다.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    <ManuStep ProdModelID = "{sql:column("Production.ProductModel.ProductModelID")}"  
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
     <Location>  
       { (//AWMI:root/AWMI:Location)[2]/@* }  
       <Steps>  
         { for $s in (//AWMI:root/AWMI:Location)[2]//AWMI:step  
           return  
              <Step>  
               { string($s) }  
              </Step>  
         }  
        </Steps>  
      </Location>  
     </ManuStep>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   중괄호 안에 있는 식은 해당 평가 결과로 대체됩니다. 자세한 내용은 [XML 생성 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)를 참조 하세요.  
  
-   **@\*** 두 번째 작업 센터 위치의 모든 특성을 검색 합니다.  
  
-   FLWOR 반복 (... RETURN)는 두 번째 작업 `step` 센터 위치의 자식 요소> 모든 <를 검색 합니다.  
  
-   [Sql: column () 함수 (XQuery)](../xquery/xquery-extension-functions-sql-column.md) 는 생성 되는 XML에 관계형 값을 포함 합니다.  
  
 다음은 결과입니다.  
  
```  
<ManuStep ProdModelID="7" ProductModelName="HL Touring Frame">  
  <Location LocationID="20" SetupHours="0.15"   
              MachineHours="2"  LaborHours="1.75" LotSize="1">  
  <Steps>  
   <Step>Assemble all frame components following blueprint 1299.</Step>  
     ...  
  </Steps>  
 </Location>  
</ManuStep>    
```  
  
 이전 쿼리에서는 단지 텍스트 노드만 검색합니다. 전체 <`step`> 요소가 대신 반환 되도록 하려면 쿼리에서 **string ()** 함수를 제거 합니다.  
  
### <a name="b-find-all-the-material-and-tools-used-at-the-second-work-center-location-in-the-manufacturing-of-a-product"></a>B. 제품 제조의 두 번째 작업 센터 위치에서 사용되는 모든 자재 및 도구 찾기  
 특정 제품 모델에 대해 다음 쿼리는 제조 프로세스의 작업 센터 위치 시퀀스에 따라 두 번째 작업 센터 위치에서 사용되는 도구와 자재를 검색합니다.  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <Location>  
      { (//AWMI:root/AWMI:Location)[1]/@* }  
       <Tools>  
         { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:tool  
           return  
              <Tool>  
                { string($s) }  
              </Tool>  
          }  
        </Tools>  
        <Materials>  
            { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:material  
              return  
                 <Material>  
                    { string($s) }  
                 </Material>  
             }  
         </Materials>  
  </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   이 쿼리는 <Loca`tion`> 요소를 생성 하 고 데이터베이스에서 해당 특성 값을 검색 합니다.  
  
-   여기에서는 두 개의 FLWOR (for...return) 반복문이 사용되며, 이 중 하나는 도구를 검색하고 다른 하나는 사용된 자재를 검색합니다.  
  
 다음은 결과입니다.  
  
```xml
<Location LocationID="10" SetupHours=".5"   
          MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
    <Tool>router with a carbide tip 15</Tool>  
    <Tool>Forming Tool FT-15</Tool>  
  </Tools>  
  <Materials>  
    <Material>aluminum sheet MS-2341</Material>  
  </Materials>  
</Location>  
```  
  
### <a name="c-retrieve-the-first-two-product-feature-descriptions-from-the-product-catalog"></a>C. 제품 카탈로그에서 처음 두 개의 제품 기능 설명 검색  
 특정 제품 모델의 경우이 쿼리는 제품 모델 카탈로그의 <`Features`> 요소에서 처음 두 개의 기능 설명을 검색 합니다.  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <ProductModel ProductModelID= "{ data( (/p1:ProductDescription/@ProductModelID)[1] ) }"  
                   ProductModelName = "{ data( (/p1:ProductDescription/@ProductModelName)[1] ) }" >  
       {  
         for $F in /p1:ProductDescription/p1:Features  
         return   
           $F/*[position() <= 2]   
       }  
     </ProductModel>  
      ') as x  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
 쿼리 본문은 제품을 포함 하는 <`ProductModel`> 요소를 포함 하는 XML을 생성 합니다.  
  
-   쿼리에서 ...를 사용 합니다. 반환 루프를 통해 제품 모델 기능 설명을 검색 합니다. **Position ()** 함수는 처음 두 기능을 검색 하는 데 사용 됩니다.  
  
 다음은 결과입니다.  
  
```xml
<ProductModel ProductModelID="19" ProductModelName="Mountain 100">  
 <p1:Warranty   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
  <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
 <p2:Maintenance   
  xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p2:NoOfYears>10</p2:NoOfYears>  
  <p2:Description>maintenance contact available through your dealer   
            or any AdventureWorks retail store.  
  </p2:Description>  
 </p2:Maintenance>  
</ProductModel>   
```  
  
### <a name="d-find-the-first-two-tools-used-at-the-first-work-center-location-in-the-manufacturing-process-of-the-product"></a>D. 제품 제조 프로세스의 첫 번째 작업 센터 위치에서 사용되는 처음 두 개의 도구 찾기  
 제품 모델에 대해 다음 쿼리는 제조 프로세스의 작업 센터 위치 시퀀스에 따라 첫 번째 작업 센터 위치에서 사용되는 처음 두 개의 도구를 반환합니다. 이 쿼리는 **Production 모델** 테이블의 **명령** 열에 저장 된 제조 지침에 따라 지정 됩니다.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   for $Inst in (//AWMI:root/AWMI:Location)[1]  
   return   
     <Location>  
       { $Inst/@* }  
       <Tools>  
         { for $s in ($Inst//AWMI:step//AWMI:tool)[position() <= 2]  
           return  
             <Tool>  
               { string($s) }  
             </Tool>  
         }  
       </Tools>  
     </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 다음은 결과입니다.  
  
```xml
<Location LocationID="10" SetupHours=".5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
  </Tools>  
</Location>   
```  
  
### <a name="e-find-the-last-two-manufacturing-steps-at-the-first-work-center-location-in-the-manufacturing-of-a-specific-product"></a>E. 특정 제품 제조의 첫 번째 작업 센터 위치에서 마지막 두 개의 제조 단계 찾기  
 이 쿼리에서는 **last ()** 함수를 사용 하 여 마지막 두 제조 단계를 검색 합니다.  
  
```sql
SELECT Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 다음은 결과입니다.  
  
```xml
<LastTwoManuSteps>  
   <Last-1Step>When finished, inspect the forms for defects per   
               Inspection Specification .</Last-1Step>  
   <LastStep>Remove the frames from the tool and place them in the   
             Completed or Rejected bin as appropriate.</LastStep>  
</LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>참고 항목  
 [XML 데이터 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 생성 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
