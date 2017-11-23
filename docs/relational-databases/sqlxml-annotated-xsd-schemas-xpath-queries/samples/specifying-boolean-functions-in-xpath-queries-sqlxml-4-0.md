---
title: "XPath 쿼리 (SQLXML 4.0) 부울 함수 지정 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], Boolean functions
- false function
- not function [SQLXML]
- true function
- Boolean functions
ms.assetid: c72cd333-9294-4d41-84f2-1748bf20e3eb
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6fa92aee30c401bc0a244a46f7e5f944c5bf8c80
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="specifying-boolean-functions-in-xpath-queries-sqlxml-40"></a>XPath 쿼리에 부울 함수 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]다음 예에서는 어떻게 부울 함수를 보여 줍니다. XPath 쿼리에서 지정 합니다. 이 예의 XPath 쿼리는 SampleSchema1.xml에 포함된 매핑 스키마에 대해 지정되었습니다. 이 예제 스키마에 대 한 정보를 참조 하십시오. [XPath 예제 &#40;에 대 한 샘플 주석이 추가 된 XSD 스키마 SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>예  
  
## <a name="a-specify-the-not-boolean-function"></a>1. not() 부울 함수 지정  
 이 쿼리 모두 반환 된  **\<고객 >** 가 없는 컨텍스트 노드의 자식 요소  **\<순서 >** 자식 요소:  
  
```  
/child::Customer[not(child::Order)]  
```  
  
 **자식** 축 값이 기본값입니다. 따라서 다음과 같이 쿼리를 지정할 수 있습니다.  
  
```  
/Customer[not(Order)]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>매핑 스키마에 대해 XPath 쿼리를 테스트하려면  
  
1.  복사는 [예제 스키마 코드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) 텍스트 파일에 붙여 넣습니다. 파일을 SampleSchema1.xml로 저장합니다.  
  
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
  
     자세한 내용은 참조 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 템플릿 실행 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
## <a name="b-specify-the-true-and-false-boolean-functions"></a>2. true() 및 false() 부울 함수 지정  
 이 쿼리 모두 반환  **\<고객 >** 가 없는 컨텍스트 노드의 요소 자식을  **\<순서 >** 자식 요소입니다. 관계적인 측면으로 설명하면 이 쿼리는 주문을 하지 않은 모든 고객을 반환합니다.  
  
```  
/child::Customer[child::Order=false()]  
```  
  
 **자식** 축 값이 기본값입니다. 따라서 다음과 같이 쿼리를 지정할 수 있습니다.  
  
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
  
1.  복사는 [예제 스키마 코드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) 텍스트 파일에 붙여 넣습니다. 파일을 SampleSchema1.xml로 저장합니다.  
  
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
  
     자세한 내용은 참조 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 템플릿 실행 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
  
