---
title: not 함수 (XQuery) | Microsoft Docs
description: XQuery not () 함수를 부울 값과 함께 사용 하는 방법에 대해 알아봅니다.
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
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
author: rothja
ms.author: jroth
ms.openlocfilehash: 24235099ec742d4c6d62e3d97ee1f551af24f7d4
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524416"
---
# <a name="functions-on-boolean-values---not-function"></a>부울 값 함수 - not 함수 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  *$Arg* 의 유효한 부울 값이 FALSE 이면 true를 반환 하 고 *$Arg* 의 유효한 부울 값이 TRUE 이면 false를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 유효한 부울 값이 있는 항목의 시퀀스입니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. Not () XQuery 함수를 사용 하 여 카탈로그 설명에 요소가 포함 되지 않은 제품 모델을 찾습니다 \<Specifications> .  
 다음 쿼리는 카탈로그 설명에 <> 요소가 포함 되지 않은 제품 모델에 대 한 제품 모델 Id를 포함 하는 XML을 생성 합니다 `Specifications` .  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
-   문서에서 네임스페이스가 사용되기 때문에 예제에는 WITH NAMESPACES 문이 사용됩니다. 또 다른 옵션은 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 의 **declare namespace** 키워드를 사용 하 여 접두사를 정의 하는 것입니다.  
  
-   그런 다음 쿼리는 <`Product`> 요소와 해당 **제품 modelid** 특성을 포함 하는 XML을 생성 합니다.  
  
-   WHERE 절은 [exist () 메서드 (XML 데이터 형식)](../t-sql/xml/exist-method-xml-data-type.md) 를 사용 하 여 행을 필터링 합니다. **Exist ()** 메서드는 \<ProductDescription> 자식 요소가 없는 요소가 있으면 True를 반환 합니다 \<Specification> . **Not ()** 함수를 사용 합니다.  
  
 각 제품 모델 카탈로그 설명에 요소가 포함 되어 있으므로이 결과 집합은 비어 있습니다 \<Specifications> .  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. not() XQuery 함수를 사용하여 MachineHours 특성이 없는 작업 센터 위치 검색  
 다음 쿼리는 Instructions 열에 대해 지정되었습니다. 이 열에는 제품 모델에 대한 제조 지침이 저장됩니다.  
  
 특정 제품 모델에 대해 이 쿼리는 MachineHours를 지정하지 않는 작업 센터 위치를 검색합니다. 즉, 요소에 대 한 특성 **Machinehours** 가 지정 되지 않았습니다 \<Location> .  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
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
  
-   [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 의 **Declarenamespace** 는 놀이 Works 제조 지침 네임 스페이스 접두사를 정의 합니다. 제조 지침 문서에 사용된 동일 네임스페이스를 나타냅니다.  
  
-   쿼리에서 **not ( @MachineHours )** 조건자는 **machinehours** 특성이 없는 경우 True를 반환 합니다.  
  
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
  
-   **Not ()** 함수는 xs: boolean, node () * 또는 빈 시퀀스 유형의 인수만 지원 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
