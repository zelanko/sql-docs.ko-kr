---
title: "value () 메서드 (xml 데이터 형식) | Microsoft Docs"
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
- value method
- value() method
ms.assetid: 298a7361-dc9a-4902-9b1e-49a093cd831d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7a3822e0469836b59369eb676ece956533d4df58
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="value-method-xml-data-type"></a>value() 메서드(xml 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  XML에 대해 XQuery를 수행하고 SQL 유형의 값을 반환합니다. 이 메서드는 스칼라 값을 반환합니다.  
  
 에 저장 된 XML 인스턴스에서 값을 추출 하려면이 메서드를 일반적으로 사용 된 **xml** 유형 열, 매개 변수 또는 변수입니다. 이 방식으로 비-XML 열에 있는 데이터와 XML 데이터를 조합 또는 비교하는 SELECT 쿼리를 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
value (XQuery, SQLType)  
```  
  
## <a name="arguments"></a>인수  
 *XQuery*  
 이 *XQuery* 식, XML 인스턴스 내의 데이터를 검색 하는 문자열 리터럴로 합니다. XQuery는 최대 하나의 값을 반환해야 합니다. 그렇지 않으면 오류가 반환됩니다.  
  
 *SQLType*  
 반환되는 기본 SQL 유형(문자열 리터럴)입니다. 이 메서드의 반환 형식이 일치는 *SQLType* 매개 변수입니다. *SQLType* 일 수 없습니다는 **xml** 데이터 형식, 공용 언어 런타임 (CLR) 사용자 정의 형식, **이미지**, **텍스트**, **ntext**, 또는 **sql_variant** 데이터 형식입니다. *SQLType* 는 SQL 사용자 정의 데이터 형식일 수 있습니다.  
  
 **value ()** 메서드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 연산자를 암시적으로 변환 하 고 로지정된해당SQL유형으로XSD형식에서serialize된문자열표현XQuery식의결과변환하려고합니다.[!INCLUDE[tsql](../../includes/tsql-md.md)] 변환 합니다. CONVERT에 대 한 캐스트 규칙에 대 한 자세한 내용은 참조 하십시오. [CAST 및 convert&#40; Transact SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
> [!NOTE]  
>  사용 하는 대신 성능상의 이유로 **value ()** 관계형 값을 사용 하 여과 비교 하는 조건자에서 메서드 **exist ()** 와 **: column ()**합니다. 뒤에 나오는 예 4에서 이러한 작업 방법을 보여 줍니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-value-method-against-an-xml-type-variable"></a>1. xml 유형 변수에 대해 value() 메서드 사용  
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
  
 XML 인스턴스에 `ProductID` 특성이 하나만 있지만 정적 형식 지정 규칙에 따라 경로 식이 단일 항목을 반환하도록 명시적으로 지정해야 합니다. 따라서 추가 항목 `[1]`은 경로 식의 끝에 지정됩니다. 정적 형식 지정에 대 한 자세한 내용은 참조 [XQuery 및 정적 형식 지정](../../xquery/xquery-and-static-typing.md)합니다.  
  
### <a name="b-using-the-value-method-to-retrieve-a-value-from-an-xml-type-column"></a>2. value() 메서드를 사용하여 xml 유형 열에서 값 검색  
 에 대해 다음 쿼리는 지정 된 **xml** 유형 열 (`CatalogDescription`)에 `AdventureWorks` 데이터베이스 합니다. 이 쿼리는 열에 저장된 각 XML 인스턴스로부터 `ProductModelID` 특성 값을 검색합니다.  
  
```  
SELECT CatalogDescription.value('             
    declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";             
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
  
### <a name="c-using-the-value-and-exist-methods-to-retrieve-values-from-an-xml-type-column"></a>3. value() 및 exist() 메서드를 사용하여 xml 유형 열로부터 값 검색  
 다음 예제에서는 모두 사용 하 여는 `value()` 메서드 및 [exist () 메서드](../../t-sql/xml/exist-method-xml-data-type.md) 의 **xml** 데이터 형식입니다. `value()` 메서드는 XML로부터 `ProductModelID` 특성 값을 검색하는 데 사용됩니다. `exist()` 절에 있는 `WHERE` 메서드는 테이블의 행을 필터링하는 데 사용됩니다.  
  
 이 쿼리는 여러 기능 중 하나로 보증 정보(<`Warranty`> 요소)가 포함된 제품 모델 ID를 XML 인스턴스로부터 검색합니다. `WHERE` 절의 조건에서는 `exist()` 메서드를 사용하여 이 조건을 만족하는 행만 검색합니다.  
  
```  
SELECT CatalogDescription.value('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           (/PD:ProductDescription/@ProductModelID)[1] ', 'int') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 이전 쿼리에서 다음을 유의하세요.  
  
-   `CatalogDescription` 열은 형식화된 XML 열입니다. 즉, 이 열에는 이와 관련된 스키마 컬렉션이 있습니다. 에 [XQuery 프롤로그](../../xquery/modules-and-prologs-xquery-prolog.md), 네임 스페이스 선언은 나중에 쿼리 본문에서에서 사용 되는 접두사를 정의 하는 사용 됩니다.  
  
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
  
### <a name="d-using-the-exist-method-instead-of-the-value-method"></a>4. value() 메서드 대신 exist() 메서드 사용  
 성능상의 이유로 조건자에서 `value()` 메서드를 사용하여 관계형 값과 비교하는 대신 `exist()`에서 `sql:column()`를 사용하세요. 예를 들어  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 데이터 수정 언어 &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
