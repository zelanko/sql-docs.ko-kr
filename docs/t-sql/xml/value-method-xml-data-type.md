---
title: value() 메서드(xml 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- value method
- value() method
ms.assetid: 298a7361-dc9a-4902-9b1e-49a093cd831d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9224e9050ecf01255151e5ec8e11ecaf282d7387
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68051222"
---
# <a name="value-method-xml-data-type"></a>value() 메서드(xml 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  XML에 대해 XQuery를 수행하고 SQL 유형의 값을 반환합니다. 이 메서드는 스칼라 값을 반환합니다.  
  
 이 메서드는 일반적으로 **xml** 유형 열, 매개 변수 또는 변수에 저장된 XML 인스턴스로부터 값을 추출하는 데 사용됩니다. 이 방식으로 비-XML 열에 있는 데이터와 XML 데이터를 조합 또는 비교하는 SELECT 쿼리를 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
value (XQuery, SQLType)  
```  
  
## <a name="arguments"></a>인수  
 *XQuery*  
 XML 인스턴스 내에서 데이터를 검색하는 *XQuery* 식(문자열 리터럴)입니다. XQuery는 최대 하나의 값을 반환해야 합니다. 그렇지 않으면 오류가 반환됩니다.  
  
 *SQLType*  
 반환되는 기본 SQL 유형(문자열 리터럴)입니다. 이 메서드의 반환 형식은 *SQLType* 매개 변수와 일치합니다. *SQLType*은 **xml** 데이터 형식, 공용 언어 런타임 (CLR) 사용자 정의 형식, **이미지**, **텍스트**, **ntext** 또는 **sql_variant** 데이터 형식일 수 없습니다. *SQLType*은 SQL 사용자 정의 데이터 형식일 수 있습니다.  
  
 **value()** 메서드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 연산자를 암시적으로 사용하고 직렬화된 문자열 표현인 XQuery 식의 결과를 XSD 유형에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 변환으로 지정된 해당 SQL 유형으로 변환하려고 시도합니다. CONVERT에 대한 형식 캐스트 규칙에 대한 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
>  성능상의 이유로 조건자에서 **value()** 메서드를 사용하여 관계형 값과 비교하는 대신 **sql:column()** 에서 **exist()** 를 사용하세요. 뒤에 나오는 예 4에서 이러한 작업 방법을 보여 줍니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-value-method-against-an-xml-type-variable"></a>A. xml 유형 변수에 대해 value() 메서드 사용  
 다음 예에서 XML 인스턴스는 `xml` 유형의 변수에 저장됩니다. `value()` 메서드는 XML에서 `ProductID` 특성 값을 검색합니다. 그런 다음 이 값은 `int` 변수에 할당됩니다.  
  
```  
DECLARE @myDoc xml  
DECLARE @ProdID int  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
  
SET @ProdID =  @myDoc.value('(/Root/ProductDescription/@ProductID)[1]', 'int' )  
SELECT @ProdID  
```  
  
 값 1이 결과로 반환됩니다.  
  
 XML 인스턴스에 `ProductID` 특성이 하나만 있지만 정적 형식 지정 규칙에 따라 경로 식이 단일 항목을 반환하도록 명시적으로 지정해야 합니다. 따라서 추가 항목 `[1]`은 경로 식의 끝에 지정됩니다. 정적 형식 지정에 대한 자세한 내용은 [XQuery 및 정적 형식 지정](../../xquery/xquery-and-static-typing.md)을 참조하세요.  
  
### <a name="b-using-the-value-method-to-retrieve-a-value-from-an-xml-type-column"></a>B. value() 메서드를 사용하여 xml 유형 열에서 값 검색  
 `AdventureWorks` 데이터베이스의 **xml** 유형 열(`CatalogDescription`)에 대해서는 다음 쿼리가 지정됩니다. 이 쿼리는 열에 저장된 각 XML 인스턴스로부터 `ProductModelID` 특성 값을 검색합니다.  
  
```  
SELECT CatalogDescription.value('             
    declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";             
       (/PD:ProductDescription/@ProductModelID)[1]', 'int') AS Result             
FROM Production.ProductModel             
WHERE CatalogDescription IS NOT NULL             
ORDER BY Result desc             
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   `namespace` 키워드는 네임스페이스 접두사를 정의하는 데 사용됩니다.  
  
-   각 정적 형식 지정 요구 사항에 따라 `[1]` 메서드에 있는 경로 식의 끝에 `value()`이 추가되어 해당 경로 식이 단일 항목을 반환함을 명시적으로 나타냅니다.  
  
 다음은 결과의 일부입니다.  
  
```  
-----------  
35           
34           
...  
```  
  
### <a name="c-using-the-value-and-exist-methods-to-retrieve-values-from-an-xml-type-column"></a>C. value() 및 exist() 메서드를 사용하여 xml 유형 열로부터 값 검색  
 다음 예에서는 **xml** 데이터 형식의 `value()` 메서드 및 [exist() 메서드](../../t-sql/xml/exist-method-xml-data-type.md)를 사용하는 방법을 보여 줍니다. `value()` 메서드는 XML로부터 `ProductModelID` 특성 값을 검색하는 데 사용됩니다. `exist()` 절에 있는 `WHERE` 메서드는 테이블의 행을 필터링하는 데 사용됩니다.  
  
 이 쿼리는 여러 기능 중 하나로 보증 정보(<`Warranty`> 요소)가 포함된 제품 모델 ID를 XML 인스턴스로부터 검색합니다. `WHERE` 절의 조건에서는 `exist()` 메서드를 사용하여 이 조건을 만족하는 행만 검색합니다.  
  
```  
SELECT CatalogDescription.value('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           (/PD:ProductDescription/@ProductModelID)[1] ', 'int') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   `CatalogDescription` 열은 형식화된 XML 열입니다. 즉, 이 열에는 이와 관련된 스키마 컬렉션이 있습니다. [XQuery 프롤로그](../../xquery/modules-and-prologs-xquery-prolog.md)에서 네임스페이스 선언은 나중에 쿼리 본문에서 사용되는 접두사를 정의하기 위해 사용됩니다.  
  
-   `exist()` 메서드가 `1`(True)을 반환하는 경우는 XML 인스턴스에 여러 기능 중 하나로 <`Warranty`> 자식 요소가 포함되어 있음을 나타냅니다.  
  
-   그런 다음 `value()` 절의 `SELECT` 메서드는 `ProductModelID` 특성 값을 정수로 검색합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
Result       
-----------  
19           
23           
...  
```  
  
### <a name="d-using-the-exist-method-instead-of-the-value-method"></a>D. value() 메서드 대신 exist() 메서드 사용  
 성능상의 이유로 조건자에서 `value()` 메서드를 사용하여 관계형 값과 비교하는 대신 `exist()`에서 `sql:column()`를 사용하세요. 다음은 그 예입니다.  
  
```  
CREATE TABLE T (c1 int, c2 varchar(10), c3 xml)  
GO  
  
SELECT c1, c2, c3   
FROM T  
WHERE c3.value( '/root[1]/@a', 'integer') = c1  
GO  
```  
  
 다음은 이에 대한 예입니다.  
  
```  
SELECT c1, c2, c3   
FROM T  
WHERE c3.exist( '/root[@a=sql:column("c1")]') = 1  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
