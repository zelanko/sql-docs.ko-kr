---
title: "not 함수 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5f64f286b59b67e31d0b49527a83409b81ba2210
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-boolean-values---not-function"></a>부울 값-함수가 아닌 함수 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  TRUE를 반환 합니다의 유효한 부울 값 *$arg* 이 false 이면 고 FALSE 이면 반환의 유효한 부울 값 *$arg* 그렇습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 유효한 부울 값이 있는 항목의 시퀀스입니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>1. Not () XQuery 함수를 사용 하 여 제품 모델 카탈로그 설명 찾기 포함 되지 않습니다는 \<사양 > 요소입니다.  
 다음 쿼리는 카탈로그 설명에 <`Specifications`> 요소가 포함되지 않은 제품 모델에 대한 제품 모델 ID가 포함되는 XML을 생성합니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
       <Product   
           ProductModelID="{ sql:column("ProductModelID") }"  
        />  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications/*)]  '  
     ) = 0  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   문서에서 네임스페이스가 사용되기 때문에 예제에는 WITH NAMESPACES 문이 사용됩니다. 다른 옵션은 사용 하는 **네임 스페이스를 선언** 키워드는 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 접두사를 정의 하 합니다.  
  
-   쿼리는 다음을 포함 하는 XML 생성은 <`Product`> 요소와 해당 **ProductModelID** 특성입니다.  
  
-   WHERE 절이 사용 하는 [exist () 메서드 (XML 데이터 형식)](../t-sql/xml/exist-method-xml-data-type.md) 된 행을 필터링 합니다. **exist ()** 메서드가 있는 경우 True를 반환 \<ProductDescription > 요소를 갖지 않는 \<사양 > 자식 요소입니다. 사용 하 여는 **not ()** 함수입니다.  
  
 이 결과 집합이 비어 각 제품 모델 카탈로그 설명에 포함 되어 있으므로 \<사양 > 요소입니다.  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>2. not() XQuery 함수를 사용하여 MachineHours 특성이 없는 작업 센터 위치 검색  
 다음 쿼리는 Instructions 열에 대해 지정되었습니다. 이 열에는 제품 모델에 대한 제조 지침이 저장됩니다.  
  
 특정 제품 모델에 대해 이 쿼리는 MachineHours를 지정하지 않는 작업 센터 위치를 검색합니다. 즉, 특성 **MachineHours** 지정 되어 있지 않은 \<위치 > 요소입니다.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in /AWMI:root/AWMI:Location[not(@MachineHours)]  
     return  
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ $i/@LaborHours }" >  
        </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7   
```  
  
 위의 코드에서 다음에 유의하십시오.  
  
-   **declarenamespace** 에 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) Adventure Works 제조 지침 네임 스페이스 접두사를 정의 합니다. 제조 지침 문서에 사용된 동일 네임스페이스를 나타냅니다.  
  
-   쿼리에서 **없습니다 (@MachineHours)** 있는 경우 True를 반환 하는 조건자 없습니다 **MachineHours** 특성입니다.  
  
 다음은 결과입니다.  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **not ()** 함수 인수 xs: boolean 유형의 node () * 또는 빈 시퀀스만 지원 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
