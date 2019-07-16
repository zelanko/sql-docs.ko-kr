---
title: XPath 쿼리 (SQLXML 4.0) 부울 함수 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], Boolean functions
- false function
- not function [SQLXML]
- true function
- Boolean functions
ms.assetid: c72cd333-9294-4d41-84f2-1748bf20e3eb
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 95569262bc55da45390705486871a73f0eb5f5ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027114"
---
# <a name="specifying-boolean-functions-in-xpath-queries-sqlxml-40"></a>XPath 쿼리에 부울 함수 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  다음 예에서는 XPath 쿼리에 부울 함수를 지정하는 방법을 보여 줍니다. 이 예의 XPath 쿼리는 SampleSchema1.xml에 포함된 매핑 스키마에 대해 지정되었습니다. 이 예제 스키마에 대 한 정보를 참조 하세요 [샘플 주석이 추가 된 XSD 스키마 XPath 예제에 대 한 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)합니다.  
  
## <a name="examples"></a>예  
  
## <a name="a-specify-the-not-boolean-function"></a>A. not() 부울 함수 지정  
 이 쿼리 모두 반환 합니다  **\<고객 >** 하지 않은 컨텍스트 노드의 자식 요소  **\<순서 >** 자식 요소:  
  
```  
/child::Customer[not(child::Order)]  
```  
  
 합니다 **자식** 축은 기본값입니다. 따라서 다음과 같이 쿼리를 지정할 수 있습니다.  
  
```  
/Customer[not(Order)]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>매핑 스키마에 대해 XPath 쿼리를 테스트하려면  
  
1.  복사 합니다 [샘플 스키마 코드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) 텍스트 파일에 붙여 넣습니다. 파일을 SampleSchema1.xml로 저장합니다.  
  
2.  다음 템플릿(BooleanFunctionsA.xml)을 만들어 SampleSchema1.xml이 저장된 디렉터리에 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Customer[not(Order)]  
    </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(SampleSchema1.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     For more information, see [Using ADO to Execute SQLXML 4.0 Queries](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 다음은 템플릿 실행 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
## <a name="b-specify-the-true-and-false-boolean-functions"></a>2\. true() 및 false() 부울 함수 지정  
 이 쿼리 모두 반환  **\<고객 >** 하지 않은 컨텍스트 노드의 요소 자식을  **\<순서 >** 자식 요소입니다. 관계적인 측면으로 설명하면 이 쿼리는 주문을 하지 않은 모든 고객을 반환합니다.  
  
```  
/child::Customer[child::Order=false()]  
```  
  
 합니다 **자식** 축은 기본값입니다. 따라서 다음과 같이 쿼리를 지정할 수 있습니다.  
  
```  
/Customer[Order=false()]  
```  
  
 이 쿼리는 다음과 같습니다.  
  
```  
/Customer[not(Order)]  
```  
  
 다음 쿼리는 주문을 한 번 이상 한 모든 고객을 반환합니다.  
  
```  
/Customer[Order=true()]  
```  
  
 이 쿼리는 다음과 같습니다.  
  
```  
/Customer[Order]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>매핑 스키마에 대해 XPath 쿼리를 테스트하려면  
  
1.  복사 합니다 [샘플 스키마 코드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) 텍스트 파일에 붙여 넣습니다. 파일을 SampleSchema1.xml로 저장합니다.  
  
2.  다음 템플릿(BooleanFunctionsB.xml)을 만들어 SampleSchema1.xml이 저장된 디렉터리에 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[Order=false()]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(SampleSchema1.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 템플릿 실행 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
  
