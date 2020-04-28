---
title: count 함수 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:count function
- count function [XQuery]
ms.assetid: a9f7131f-23e1-4d4d-a36c-180447543926
author: rothja
ms.author: jroth
ms.openlocfilehash: a359251dbb2bd2a2685e5d9fb91d5c1603950c25
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67986308"
---
# <a name="aggregate-functions---count"></a>집계 함수 - count
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  *$Arg*에서 지정한 시퀀스에 포함 된 항목 수를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:count($arg as item()*) as xs:integer  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 수를 셀 항목입니다.  
  
## <a name="remarks"></a>설명  
 *$Arg* 빈 시퀀스인 경우 0을 반환 합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-count-xquery-function-to-count-the-number-of-work-center-locations-in-the-manufacturing-of-a-product-model"></a>A. count() XQuery 함수를 사용하여 제품 모델 제조의 작업 센터 위치 수 계산  
 다음 쿼리에서는 제품 모델(ProductModelID=7)의 제조 프로세스에서 작업 센터 위치 수를 계산합니다.  
  
```  
SELECT Production.ProductModel.ProductModelID,   
       Production.ProductModel.Name,   
       Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations>  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID=7  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 의 **namespace** 키워드는 네임 스페이스 접두사를 정의 합니다. 그러면 XQuery 본문에 접두사가 사용됩니다.  
  
-   이 쿼리는 <`NoOfWorkStations`> 요소를 포함 하는 XML을 생성 합니다.  
  
-   XQuery 본문의 **count ()** 함수는 <`Location`> 요소 수를 계산 합니다.  
  
 다음은 결과입니다.  
  
```  
ProductModelID   Name                 WorkCtrCount       
-------------- ---------------------------------------------------  
7             HL Touring Frame  <NoOfWorkStations>6</NoOfWorkStations>     
```  
  
 다음 쿼리와 같이 제품 모델 ID와 이름을 포함하도록 XML을 생성할 수도 있습니다.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
 다음 쿼리와 같이 XML 대신 이러한 값을 비-xml 유형으로 반환할 수도 있습니다. 이 쿼리에서는 [value () 메서드 (xml 데이터 형식)](../t-sql/xml/value-method-xml-data-type.md) 를 사용 하 여 작업 센터 위치 수를 검색 합니다.  
  
```  
SELECT  ProductModelID,   
        Name,   
        Instructions.value('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
