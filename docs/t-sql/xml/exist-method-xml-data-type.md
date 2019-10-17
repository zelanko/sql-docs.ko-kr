---
title: exist() 메서드(xml 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9621d6be1c309930f6104d2193d6127a3167cd7a
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278149"
---
# <a name="exist-method-xml-data-type"></a>exist() 메서드(xml 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  다음 경우 중 하나를 나타내는 **bit**를 반환합니다.  
  
-   쿼리의 XQuery 식이 비어 있지 않은 결과를 반환하면 True를 나타내는 1입니다. 즉 하나 이상의 XML 노드를 반환합니다.  
  
-   빈 결과를 반환하면 False를 나타내는 0입니다.  
  
-   쿼리가 실행된 **xml** 데이터 형식 인스턴스에 NULL이 있으면 NULL입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
exist (XQuery)   
```  
  
## <a name="arguments"></a>인수  
 XQuery  
 문자열 리터럴인 XQuery 식입니다.  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]  
>  **exist()** 메서드는 비어 있지 않은 결과를 반환하는 XQuery 식에 대해 1을 반환합니다. **exist()** 메서드 내에서 **true()** 또는 **false()** 함수를 지정하면 **true()** 및 **false()** 함수가 각각 부울 값인 True와 False를 반환하기 때문에 **exist()** 메서드가 1을 반환합니다. 즉, 이들 함수는 비어 있지 않은 결과를 반환합니다. 따라서 **exist()** 는 다음 예에서와 같이 1(True)을 반환합니다.  
  
```  
declare @x xml;  
set @x='';  
select @x.exist('true()');   
```  
  
## <a name="examples"></a>예  
 다음 예에서는 **exist()** 메서드를 지정하는 방법을 보여 줍니다.  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>예: xml 형식의 변수에 대해 exist() 메서드 지정  
 다음 예에서 @x는 **xml** 형식 변수(형식화되지 않은 xml)이고 @f는 **exist()** 메서드에서 반환한 값을 저장하는 정수 형식 변수입니다. XML 인스턴스에 저장된 날짜 값이 `2002-01-01`이면 **exist()** 메서드가 True(1)를 반환합니다.  
  
```  
declare @x xml;  
declare @f bit;  
set @x = '<root Somedate = "2002-01-01Z"/>';  
set @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
select @f;  
```  
  
 **exist()** 메서드의 날짜를 비교할 때 다음에 유의하세요.  
  
-   비교를 위해 값을 **xs:date** 형식으로 캐스팅하는 데 `cast as xs:date?` 코드가 사용됩니다.  
  
-   **\@Somedate** 특성의 값은 형식화되지 않습니다. 이 값을 비교할 때 암시적으로 오른쪽에 있는 형식인 **xs:date** 형식으로 캐스팅됩니다.  
  
-   **cast as xs:date()** 대신 **xs:date()** 생성자 함수를 사용할 수 있습니다. 자세한 내용은 [생성자 함수&#40;XQuery&#41;](../../xquery/constructor-functions-xquery.md)를 참조하세요.  
  
 다음 예제는 <`Somedate`> 요소가 있다는 점을 제외하고 앞의 예와 비슷합니다.  
  
```  
DECLARE @x xml;  
DECLARE @f bit;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   **text()** 메서드는 형식화되지 않은 값 `2002-01-01`을 포함하는 텍스트 노드를 반환합니다. (XQuery 형식은 **xdt:untypedAtomic**입니다.) 이 경우 암시적 캐스트가 지원되지 않으므로 **x**에서 **xsd:date**로 이 형식화된 값을 명시적으로 캐스팅해야 합니다.  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>예: 형식화된 xml 변수에 대해 exist() 메서드 지정  
 다음 예에서는 **xml** 형식 변수에 대해 **exist()** 메서드를 사용하는 방법을 보여 줍니다. 이 메서드는 스키마 네임스페이스 컬렉션 이름인 `ManuInstructionsSchemaCollection`을 지정하므로 형식화된 XML 변수입니다.  
  
 다음 예에서는 제조 지침 문서를 이 변수에 할당한 다음, **exist()** 메서드를 사용하여 **LocationID** 특성 값이 50인 <`Location`> 요소가 문서에 있는지 확인합니다.  
  
 제조 지침 문서에 `LocationID=50`을 가진 <`Location`> 요소가 포함되면 @x 변수에 대해 지정된 **exist()** 메서드가 1(True)을 반환합니다. 그렇지 않으면 메서드가 0(False)을 반환합니다.  
  
```  
DECLARE @x xml (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f int;  
SET @f = @x.exist(' declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>예: xml 형식 열에 대해 exist() 메서드 지정  
 다음 쿼리에서는 카탈로그 설명에 사양 <`Specifications`> 요소가 없는 제품 모델 ID를 검색합니다.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   WHERE 절은 **CatalogDescription xml** 형식 열에 대해 지정된 조건을 만족하는 **ProductDescription** 테이블의 행만 선택합니다.  
  
-   XML에 <`Specifications`> 요소가 없으면 WHERE 절의 **exist()** 메서드가 1(True)을 반환합니다. [not() 함수(XQuery)](../../xquery/functions-on-boolean-values-not-function.md) 사용에 유의하세요.  
  
-   비-XML 열에서 값을 가져오기 위해 [sql:column() 함수(XQuery)](../../xquery/xquery-extension-functions-sql-column.md)가 사용됩니다.  
  
-   이 쿼리는 빈 행 집합을 반환합니다.  
  
 쿼리에서 xml 데이터 형식의 **query()** 및 **exist()** 메서드를 지정하고 두 메서드는 쿼리 프롤로그에 같은 네임스페이스를 선언합니다. 이 경우 WITH XMLNAMESPACES를 사용하여 접두사를 선언하고 이 접두사를 쿼리에 사용할 수 있습니다.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
## <a name="see-also"></a>참고 항목  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
