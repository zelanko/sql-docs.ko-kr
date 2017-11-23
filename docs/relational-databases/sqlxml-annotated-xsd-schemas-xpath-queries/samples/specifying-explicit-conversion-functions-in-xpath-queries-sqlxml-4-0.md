---
title: "명시적 변환 함수를 지정 하는 XPath 쿼리 (SQLXML 4.0) | Microsoft Docs"
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
- explicit conversion functions [SQLXML]
- string function
- number function
- XPath queries [SQLXML], explicit conversion functions
ms.assetid: 1111cb5d-2bd9-4bdb-8de2-dc0e47452dd6
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e73e80583af61899d2ed8b219861c7a2868ec96a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-40"></a>XPath 쿼리에 명시적 변환 함수 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]다음 예제에서는 XPath 쿼리에 함수를 지정 하는 방법을 명시적 변환을 보여 줍니다. 이 예의 XPath 쿼리는 SampleSchema1.xml에 포함된 매핑 스키마에 대해 지정되었습니다. 이 예제 스키마에 대 한 정보를 참조 하십시오. [XPath 예제 &#40;에 대 한 샘플 주석이 추가 된 XSD 스키마 SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>예  
  
### <a name="a-use-the-number-explicit-conversion-function"></a>1. number() 명시적 변환 함수 사용  
 **number ()** 함수는 인수를 숫자로 변환 합니다.  
  
 값을 가정 **ContactID** 이 숫자가 아니라고 다음 쿼리는 변환 **ContactID** 숫자로 하며 값 4와 비교 합니다. 쿼리에서 모든 반환  **\<직원 >** 인 컨텍스트 노드의 요소 자식을 **ContactID** 4의 숫자 값이 있는 특성:  
  
```  
/child::Contact[number(attribute::ContactID)= 4]  
```  
  
 바로 가기는 **특성** 축 (@)를 지정할 수 때문이 **자식** 축은 기본값, 쿼리에서 생략 될 수 있습니다:  
  
```  
/Contact[number(@ContactID) = 4]  
```  
  
 관계에 따라에서 쿼리 인 직원을 반환는 **ContactID** 4입니다.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>매핑 스키마에 대해 XPath 쿼리를 테스트하려면  
  
1.  복사는 [예제 스키마 코드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) 텍스트 파일에 붙여 넣습니다. 파일을 SampleSchema1.xml로 저장합니다.  
  
2.  다음 템플릿(ExplicitConversionA.xml)을 만들어 SampleSchema1.xml이 저장된 디렉터리에 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Contact[number(@ContactID)=4]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(SampleSchema1.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 참조 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 이 템플릿 실행의 결과 집합입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
### <a name="b-use-the-string-explicit-conversion-function"></a>2. string() 명시적 변환 함수 사용  
 **string ()** 함수는 인수를 문자열로 변환 합니다.  
  
 다음 쿼리는 변환 **ContactID** 문자열과 비교를 사용 하 여 문자열 값 "4"입니다. 모든 쿼리 반환  **\<직원 >** 인 컨텍스트 노드의 요소 자식을 **ContactID** 문자열 값이 "4" 인:  
  
```  
/child::Contact[string(attribute::ContactID)="4"]  
```  
  
 바로 가기는 **특성** 축 (@)를 지정할 수 때문이 **자식** 축은 기본값, 쿼리에서 생략 될 수 있습니다:  
  
```  
/Contact[string(@ContactID)="4"]  
```  
  
 이 쿼리는 숫자 값(즉, 숫자 4)이 아닌 문자열 값에 대해 계산을 수행하지만 기능적으로 앞의 예제 쿼리와 동일한 결과를 반환합니다.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>매핑 스키마에 대해 XPath 쿼리를 테스트하려면  
  
1.  복사는 [예제 스키마 코드](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) 텍스트 파일에 붙여 넣습니다. 파일을 SampleSchema1.xml로 저장합니다.  
  
2.  다음 템플릿(ExplicitConversionB.xml)을 만들어 SampleSchema1.xml이 저장된 디렉터리에 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Contact[string(@ContactID)="4"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(SampleSchema1.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 참조 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 템플릿 실행의 결과 집합입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
  
