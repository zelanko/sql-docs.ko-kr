---
title: XPath 쿼리에 관계형 연산자 사용 (SQLXML)
description: SQLXML 4.0 XPath 쿼리에서 관계형 연산자를 사용 하는 방법에 대해 알아봅니다.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], relational operators
- relational operators [SQLXML]
- XPath operators [SQLXML]
- operators [SQLXML]
ms.assetid: 177a0eb2-11ef-4459-a317-485a433ee769
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dfc120a7cacea4d8eb9908d441cb1a47fa986acb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97430488"
---
# <a name="specifying-relational-operators-in-xpath-queries-sqlxml-40"></a>XPath 쿼리에 관계형 연산자 지정(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  다음 예에서는 XPath 쿼리에 관계형 연산자를 지정하는 방법을 보여 줍니다. 이 예의 XPath 쿼리는 SampleSchema1.xml에 포함된 매핑 스키마에 대해 지정되었습니다. 이 샘플 스키마에 대 한 자세한 내용은 [예제 주석 XSD schema For XPath 예제 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)를 참조 하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-specify-relational-operator"></a>A. 관계형 연산자 지정  
 이 XPath 쿼리는 **\<Customer>** **CustomerID** 특성 값이 "1"이 고 모든 자식 **\<Order>** 요소에 값이 **\<OrderDetail>** 3 보다 큰 **OrderQty** 특성을 가진 자식이 포함 된 요소의 자식 요소를 반환 합니다.  
  
```  
/child::Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
```  
  
 대괄호에 지정 된 조건자는 요소를 필터링 합니다 **\<Customer>** . **\<Customer>** **\<OrderDetail>** OrderQty 특성 값이 3 보다 큰 손자가 하나 이상 있는 요소만 반환 됩니다.  
  
 **자식** 축이 기본값입니다. 따라서 다음과 같이 쿼리를 지정할 수 있습니다.  
  
```  
/Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>매핑 스키마에 대해 XPath 쿼리를 테스트하려면  
  
1.  [샘플 스키마 코드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) 를 복사 하 여 텍스트 파일에 붙여 넣습니다. 파일을 SampleSchema1.xml로 저장합니다.  
  
2.  다음 템플릿(SpecifyRelationalA.xml)을 만들어 SampleSchema1.xml이 저장된 디렉터리에 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(SampleSchema1.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  

     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 템플릿 실행의 결과 집합입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <OrderDetail ProductID="Prod-760" UnitPrice="503.3507" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-763" UnitPrice="503.3507" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-766" UnitPrice="503.3507" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-732" UnitPrice="440.1742" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-757" UnitPrice="1049.7528" OrderQty="4" UnitPriceDiscount="0" />   
</ROOT>  
```  
  
### <a name="b-specify-relational-operator-in-the-xpath-query-and-use-boolean-function-to-compare-the-result"></a>B. XPath 쿼리에 관계형 연산자 지정 및 부울 함수를 사용하여 결과 비교  
 이 쿼리는 **\<Order>** **SalesPersonID** 특성 값이 270 보다 작은 컨텍스트 노드의 모든 요소 자식을 반환 합니다.  
  
```  
/child::Customer/child::Order[(attribute::SalesPersonID < 270)=true()]  
```  
  
 **특성** 축에 대 한 바로 가기 (@)를 지정할 수 있으며, **자식** 축이 기본값 이므로 쿼리에서 생략할 수 있습니다.  
  
```  
/Customer/Order[(@SalesPersonID < 270)=true()]  
```  
  
> [!NOTE]  
>  이 쿼리를 템플릿에서 지정 하는 경우 < 문자는 XML 문서에서 특별 한 의미가 있기 때문에 < 문자는 엔터티 인코딩 이어야 합니다. 템플릿에서 `<` < 문자를 지정 하는 데 사용 합니다.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>매핑 스키마에 대해 XPath 쿼리를 테스트하려면  
  
1.  [샘플 스키마 코드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) 를 복사 하 여 텍스트 파일에 붙여 넣습니다. 파일을 SampleSchema1.xml로 저장합니다.  
  
2.  다음 템플릿(SpecifyRelationalB.xml)을 만들어 SampleSchema1.xml이 저장된 디렉터리에 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="SampleSchema1.xml">  
            /Customer/Order[(@SalesPersonID<270)=true()]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(SampleSchema1.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 템플릿 실행 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="Ord-46613" SalesPersonID="268"   
         OrderDate="2002-07-01T00:00:00"   
         DueDate="2002-07-13T00:00:00"   
         ShipDate="2002-07-08T00:00:00">  
    <OrderDetail ProductID="Prod-739" UnitPrice="917.9363"   
                 OrderQty="2" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-779" UnitPrice="1491.4221"   
                 OrderQty="1" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-825" UnitPrice="242.1391"   
                 OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
  <Order SalesOrderID="Ord-71919" SalesPersonID="268"  
         OrderDate="2004-06-01T00:00:00"   
         DueDate="2004-06-13T00:00:00"   
         ShipDate="2004-06-08T00:00:00">  
    <OrderDetail ProductID="Prod-961" UnitPrice="534.492"   
                 OrderQty="1" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-965" UnitPrice="534.492"   
                 OrderQty="1" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-966" UnitPrice="1716.5304"   
                 OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
  ...  
</ROOT>  
```  
  
  
