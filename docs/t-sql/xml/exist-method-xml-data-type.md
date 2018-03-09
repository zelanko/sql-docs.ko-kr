---
title: "exist () 메서드 (xml 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 74fc65730d0c46858c282b9625c86d1ab651ec49
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="exist-method-xml-data-type"></a>exist() 메서드(xml 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  반환 된 **비트** 다음 조건 중 하나를 나타내는입니다.  
  
-   쿼리의 XQuery 식이 비어 있지 않은 결과를 반환하면 True를 나타내는 1입니다. 즉 하나 이상의 XML 노드를 반환합니다.  
  
-   빈 결과를 반환하면 False를 나타내는 0입니다.  
  
-   Null 인 경우는 **xml** 쿼리가 실행 되는 데이터 형식 인스턴스에 NULL이 포함 되어 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
exist (XQuery)   
```  
  
## <a name="arguments"></a>인수  
 XQuery  
 문자열 리터럴인 XQuery 식입니다.  
  
## <a name="remarks"></a>주의  
  
> [!NOTE]  
>  **exist ()** 메서드는 비어 있지 않은 결과 반환 하는 XQuery 식에 대 한 1을 반환 합니다. 지정 하는 경우는 **true ()** 또는 **false ()** 내부 함수는 **exist ()** 메서드는 **exist ()** 메서드는 1을 반환 하기 때문에 함수 **true ()** 및 **false ()** 각각 부울 값인 True와 False를 반환 합니다. 즉, 이들 함수는 비어 있지 않은 결과를 반환합니다. 따라서 **exist ()** 다음 예제와 같이 1 (True)을 반환 합니다.  
  
```  
declare @x xml;  
set @x='';  
select @x.exist('true()');   
```  
  
## <a name="examples"></a>예  
 다음 예제에서는 지정 하는 방법을 보여는 **exist ()** 메서드.  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>예제: xml 유형 변수에 대해 exist () 메서드 지정  
 다음 예에서 @x 는 **xml** 유형 변수 (형식화 되지 않은 xml) 및 @f 에서 반환 된 값을 저장 하는 정수 형식 변수는 **exist ()** 메서드. **exist ()** 메서드는 XML 인스턴스에 저장 된 날짜 값이 True (1)를 반환 `2002-01-01`합니다.  
  
```  
declare @x xml;  
declare @f bit;  
set @x = '<root Somedate = "2002-01-01Z"/>';  
set @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
select @f;  
```  
  
 날짜를 비교할는 **exist ()** 메서드를 다음을 유의 하십시오.  
  
-   코드 `cast as xs:date?` 값을 캐스팅 하는 데 사용 되 **xs: date** 유형의 위해 비교 합니다.  
  
-   값은  **@Somedate**  특성은 형식화 되지 않습니다. 이 값을 비교할 때 비교의 오른쪽에 형식으로 캐스팅할 암시적으로는 **xs: date** 유형입니다.  
  
-   대신 **xs:date()로 캐스팅**를 사용할 수 있습니다는 **xs:date()** 생성자 함수입니다. 자세한 내용은 참조 [생성자 함수 &#40; XQuery &#41; ](../../xquery/constructor-functions-xquery.md).  
  
 다음 예는 <`Somedate`> 요소가 있다는 점을 제외하고 앞의 예와 비슷합니다.  
  
```  
DECLARE @x xml;  
DECLARE @f bit;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **text ()** 형식화 되지 않은 값이 포함 된 텍스트 노드를 반환 하는 메서드 `2002-01-01`합니다. (XQuery 형식은 **xdt: untypedatomic**.) 이 형식화 된 값을 명시적으로 캐스팅 해야 **x** 를 **xsd: date**암시적 캐스트는이 경우에 지원 되지 않으므로, 합니다.  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>예제: 형식화 된 xml 변수에 대해 exist () 메서드 지정  
 다음 예제에서는 **exist ()** 에 대 한 메서드는 **xml** 유형 변수입니다. 이 메서드는 스키마 네임스페이스 컬렉션 이름인 `ManuInstructionsSchemaCollection`을 지정하므로 형식화된 XML 변수입니다.  
  
 예제에서는 문서 처음이 변수에 할당 된 제조 지침 차례로 **exist ()** 메서드는 문서에 포함 되어 있는지 여부를 찾는 데 사용 됩니다는 <`Location`> 요소를 **LocationID**  특성 값은 50입니다.  
  
 **exist ()** 에 대해 지정 된 메서드는 @x 경우 변수는 1 (True)을 반환 제조 지침 문서에 포함 되어는 <`Location`> 있는 요소로 `LocationID=50`합니다. 그렇지 않으면 메서드가 0(False)을 반환합니다.  
  
```  
DECLARE @x xml (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f int;  
SET @f = @x.exist(' declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>예제: xml 유형 열에 대해 exist () 메서드 지정  
 다음 쿼리에서는 카탈로그 설명에 사양 <`Specifications`> 요소가 없는 제품 모델 ID를 검색합니다.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   행만 선택 하는 WHERE 절은 **ProductDescription** 테이블에 대해 지정 된 조건을 만족 하는 **CatalogDescription xml** 유형 열입니다.  
  
-   **exist ()** WHERE 절 XML 하나 포함 되지 않은 경우 1 (True)을 반환 메서드 <`Specifications`> 요소입니다. 사용 하 여는 [not () 함수 (XQuery)](../../xquery/functions-on-boolean-values-not-function.md)합니다.  
  
-   [: column () 함수 (XQuery)](../../xquery/xquery-extension-functions-sql-column.md) 함수는 비-XML 열에서 값 가져오는 하는 데 사용 됩니다.  
  
-   이 쿼리는 빈 행 집합을 반환합니다.  
  
 이 쿼리는 지정 **query ()** 및 **exist ()** xml 데이터 형식의 메서드 및 이러한 두 메서드는 쿼리 프롤로그에 같은 네임 스페이스를 선언 합니다. 이 경우 WITH XMLNAMESPACES를 사용하여 접두사를 선언하고 이 접두사를 쿼리에 사용할 수 있습니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 데이터 수정 언어 &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
