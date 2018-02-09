---
title: "count 함수 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:count function
- count function [XQuery]
ms.assetid: a9f7131f-23e1-4d4d-a36c-180447543926
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 33f4a34f7c4310fa1513bd90d3dabb9438d1fcb4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="aggregate-functions---count"></a>Count 집계 함수-
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  에 지정 된 시퀀스에 포함 된 항목 수를 반환 합니다. *$arg*합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:count($arg as item()*) as xs:integer  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 수를 셀 항목입니다.  
  
## <a name="remarks"></a>주의  
 0을 반환 *$arg* 빈 시퀀스입니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-count-xquery-function-to-count-the-number-of-work-center-locations-in-the-manufacturing-of-a-product-model"></a>1. count() XQuery 함수를 사용하여 제품 모델 제조의 작업 센터 위치 수 계산  
 다음 쿼리에서는 제품 모델(ProductModelID=7)의 제조 프로세스에서 작업 센터 위치 수를 계산합니다.  
  
```  
SELECT Production.ProductModel.ProductModelID,   
       Production.ProductModel.Name,   
       Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations>  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **네임 스페이스** 키워드 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 네임 스페이스 접두사를 정의 합니다. 그러면 XQuery 본문에 접두사가 사용됩니다.  
  
-   쿼리가 <`NoOfWorkStations`> 요소를 포함하는 XML을 생성합니다.  
  
-   **count ()** 수가 XQuery 본문 개수에 함수 <`Location`> 요소입니다.  
  
 다음은 결과입니다.  
  
```  
ProductModelID   Name                 WorkCtrCount       
-------------- ---------------------------------------------------  
7             HL Touring Frame  <NoOfWorkStations>6</NoOfWorkStations>     
```  
  
 다음 쿼리와 같이 제품 모델 ID와 이름을 포함하도록 XML을 생성할 수도 있습니다.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations  
             ProductModelID= "{ sql:column("Production.ProductModel.ProductModelID") }"   
             ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID= 7  
```  
  
 다음은 결과입니다.  
  
```  
<NoOfWorkStations ProductModelID="7"   
                  ProductModelName="HL Touring Frame">6</NoOfWorkStations>  
```  
  
 다음 쿼리와 같이 XML 대신 이러한 값을 비-xml 유형으로 반환할 수도 있습니다. 쿼리에서 사용 하 여는 [value () 메서드 (xml 데이터 형식)](../t-sql/xml/value-method-xml-data-type.md) 작업 센터 위치 수를 검색할 수 있습니다.  
  
```  
SELECT  ProductModelID,   
        Name,   
        Instructions.value('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
           count(/AWMI:root/AWMI:Location)', 'int' ) as WorkCtrCount  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 다음은 결과입니다.  
  
```  
ProductModelID    Name            WorkCtrCount  
-------------- ---------------------------------  
7              HL Touring Frame        6     
```  
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
