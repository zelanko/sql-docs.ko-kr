---
title: 지침 및 제한의 XML 대량 로드 (SQLXML 4.0) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 329fb8df41df5d97cfcc3750c2850d03278d3739
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013435"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>XML 대량 로드에 대한 지침 및 제한 사항(SQLXML 4.0)
  XML 대량 로드를 사용하려면 다음의 지침과 제한 사항을 알아 두어야 합니다.  
  
-   인라인 스키마는 지원되지 않습니다.  
  
     원본 XML 문서에 인라인 스키마가 있는 경우 XML 대량 로드에서 해당 스키마를 무시합니다. XML 데이터 외부의 XML 대량 로드에 대한 매핑 스키마를 지정합니다. 매핑 스키마에서 노드를 사용 하 여 지정할 수 없습니다는 **xmlns = "x: 스키마"** 특성.  
  
-   XML 문서는 형식만 검사되고 유효성은 검사되지 않습니다.  
  
     XML 대량 로드 XML이 World Wide Web Consortium의 XML 1.0 권장 사항의 구문 요구 사항을 준수 하는지 확인 하려면 XML 문서가 잘 formed는 인지 확인 하는 것을 확인 합니다. 문서 형식이 올바르지 않으면 XML 대량 로드에서 처리가 취소되고 오류가 반환됩니다. 그러나 문서가 조각인 경우(예: 문서에 단일 루트 요소가 없는 경우)에만 예외적으로 형식이 올바르지 않은 문서도 로드됩니다.  
  
     XML 대량 로드는 XML 데이터 파일 안에 정의되거나 참조되는 XML 데이터 또는 DTD 스키마와 관련하여 문서의 유효성을 검사하지 않습니다. 또한 XML 대량 로드에서는 제공된 매핑 스키마를 기준으로 XML 데이터 파일의 유효성을 검사하지 않습니다.  
  
-   모든 XML 프롤로그 정보는 무시됩니다.  
  
     전과 후 모든 정보를 무시 하는 XML 대량 로드는 \<루트 > XML 문서의 요소입니다. 예를 들어 모든 XML 선언, 내부 DTD 정의, 외부 DTD 참조, 주석 등은 무시됩니다.  
  
-   두 테이블(예: Customer 테이블과 CustOrder 테이블) 간의 기본 키/외래 키 관계를 정의하는 매핑 스키마가 있는 경우, 스키마에서 기본 키가 들어 있는 테이블 설명이 먼저 나오고 외래 키 열이 들어 있는 테이블이 그 다음에 나와야 합니다. 이는 테이블 스키마에 식별 되는 순서는 데이터베이스에 로드 하는 데 사용 되는 순서입니다. 예를 들어, 다음과 같은 XDR 스키마 하면 오류가 발생 하기 때문에 XML 대량 로드에 사용 된  **\<순서 >** 전에 설명 하는 요소는  **\<고객 >** 요소입니다. 여기서 CustOrder의 CustomerID 열은 Cust 테이블의 CustomerID 기본 키 열을 참조하는 외래 키 열입니다.  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
        <ElementType name="Order" sql:relation="CustOrder" >  
          <AttributeType name="OrderID" />  
          <AttributeType name="CustomerID" />  
          <attribute type="OrderID" />  
          <attribute type="CustomerID" />  
        </ElementType>  
  
       <ElementType name="CustomerID" dt:type="int" />  
       <ElementType name="CompanyName" dt:type="string" />  
       <ElementType name="City" dt:type="string" />  
  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
       <ElementType name="Customers" sql:relation="Cust"   
                         sql:overflow-field="OverflowColumn"  >  
          <element type="CustomerID" sql:field="CustomerID" />  
          <element type="CompanyName" sql:field="CompanyName" />  
          <element type="City" sql:field="City" />  
          <element type="Order" >   
               <sql:relationship  
                   key-relation="Cust"  
                    key="CustomerID"  
                    foreign-key="CustomerID"  
                    foreign-relation="CustOrder" />  
          </element>  
       </ElementType>  
    </Schema>  
    ```  
  
-   스키마에서 `sql:overflow-field` 주석을 사용하여 오버플로 열을 지정하지 않으면 XML 대량 로드는 XML 문서에는 있지만 매핑 스키마에는 설명되지 않은 모든 데이터를 무시합니다.  
  
     XML 대량 로드는 알려진 태그가 XML 데이터 스트림에서 발견될 때마다 사용자가 지정한 매핑 스키마를 적용합니다. 그러나 XML 문서에는 포함되었지만 스키마에 설명되지 않은 데이터는 무시합니다. 예를 들어 설명 하는 매핑 스키마를가지고 있는  **\<고객 >** 요소. XML 데이터 파일에는  **\<AllCustomers >** 루트 태그 (스키마에 설명 되지 않은) 모두 포함 하는  **\<고객 >** 요소.  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     XML 대량 로드에서 무시 하는 경우에  **\<AllCustomers >** 요소에 매핑 시작 된  **\<고객 >** 요소. XML 대량 로드는 XML 문서에는 있지만 스키마에는 설명되어 있지 않은 모든 요소를 무시합니다.  
  
     다른 XML 원본 파일을 포함 하십시오  **\<주문 >** 요소. 이러한 요소는 매핑 스키마에 설명되어 있지 않습니다.  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      ...  
    </AllCustomers>  
    ```  
  
     XML 대량 로드는 이러한 무시  **\<주문 >** 요소. 하지만 사용 하는 경우는 `sql:overflow-field`이 칼럼에서 사용 되지 않은 모든 데이터를 저장 하는 XML 대량 로드는 오버플로 열으로 열을 식별 하는 스키마에서 주석입니다.  
  
-   CDATA 섹션과 엔터티 참조는 데이터베이스에 저장되기 전에 해당하는 문자열로 변환됩니다.  
  
     이 예제에서는 CDATA 섹션 값을 래핑하는  **\<도시 >** 요소. 삽입 하기 전에 문자열 값 ("NY") 추출 하는 XML 대량 로드는  **\<도시 >** 요소를 데이터베이스에 있습니다.  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML 대량 로드는 엔터티 참조를 유지하지 않습니다.  
  
-   매핑 스키마에서 특성의 기본값을 지정하고 XML 원본 데이터에 해당 특성이 없으면, XML 대량 로드는 기본값을 사용합니다.  
  
     다음 예제 XDR 스키마에 기본값을 할당 된 **HireDate** 특성:  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
  
       <ElementType name="Customers" sql:relation="Cust3" >  
          <AttributeType name="CustomerID" dt:type="int"  />  
          <AttributeType name="HireDate"  default="2000-01-01" />  
          <AttributeType name="Salary"   />  
  
          <attribute type="CustomerID" sql:field="CustomerID" />  
          <attribute type="HireDate"   sql:field="HireDate"  />  
          <attribute type="Salary"     sql:field="Salary"    />  
       </ElementType>  
    </Schema>  
    ```  
  
     이 XML 데이터는 **HireDate** 두 번째 특성이 없는  **\<고객 >** 요소. 두 번째 XML 대량 로드에서 삽입 하는 경우  **\<고객 >** 데이터베이스에 요소를 스키마에 지정 된 기본값이 사용 됩니다.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   `sql:url-encode` 주석은 지원되지 않습니다.  
  
     XML 데이터 입력에 URL을 지정하면 대량 로드는 해당 위치에서 데이터를 읽지 못합니다.  
  
     매핑 스키마에 식별된 테이블이 생성됩니다(데이터베이스가 존재해야 함). 테이블 중 하나 이상이 데이터베이스에 이미 있으면 SGDropTables 속성은 기존의 테이블 삭제 하 고 다시 생성 되는지 여부를 결정 합니다.  
  
-   SchemaGen 속성을 지정 하는 경우 (SchemaGen 예를 들어, = true), 매핑 스키마에 식별 된 테이블이 생성 됩니다. 하지만 SchemaGen 예외적으로이 테이블에서 모든 제약 조건 (예: PRIMARY KEY/FOREIGN KEY 제약 조건)을 만들지 않습니다. 관계의 기본 키를 구성 하는 XML 노드 ID의 XML 형식으로 정의 된 경우 (즉, `type="xsd:ID"` XSD에 대 한) SGUseID 속성 SchemaGen True로 설정 되 고 뿐만 아니라 기본 키가 생성 ID의 노드를 입력 합니다. 있지만 매핑 스키마 관계에서 기본 키/외래 키 관계가 생성 됩니다.  
  
-   SchemaGen 사용 하지 않는 확장 스키마 패싯을 XSD 및 관계형 생성 하 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 스키마입니다.  
  
-   SchemaGen 속성을 지정 (SchemaGen 예를 들어, = true)을 대량 로드만 (테이블과 뷰 공유 이름) 지정 된 업데이트 됩니다.  
  
-   SchemaGen은 주석이 추가 된 XSD에서 관계형 스키마를 생성 하기 위한 기본 기능을 제공 합니다. 필요한 경우 생성된 테이블을 사용자가 직접 수정해야 합니다.  
  
-   테이블 간에 이상의 관계가 있는 SchemaGen 두 테이블 간에 관련 된 모든 키를 포함 하는 단일 관계를 만들려고 합니다. 이 제한 사항은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 오류의 원인이 될 수 있습니다.  
  
-   XML 데이터를 데이터베이스에 대량 로드할 경우 데이터베이스 열에 매핑되는 특성 또는 자식 요소가 매핑 스키마에 적어도 하나 있어야 합니다.  
  
-   XML 대량 로드를 사용하여 날짜 값을 삽입할 경우 값을 (-)CCYY-MM-DD((+-)TZ) 형식으로 지정해야 합니다. 이 형식은 날짜에 대한 표준 XSD 형식입니다.  
  
-   일부 속성 플래그는 다른 속성 플래그와 함께 사용할 수 없습니다. 예를 들어 대량 로드는 `Ignoreduplicatekeys=true`와 `Keepidentity=false`를 동시에 지원하지 않습니다. `Keepidentity=false`이면 대량 로드에서는 서버를 통해 키 값이 생성되는 것으로 간주합니다. 테이블에는 키에 대한 `IDENTITY` 제약 조건이 있어야 합니다. 서버에서는 중복 키를 생성하지 않으므로 `Ignoreduplicatekeys`를 `true`로 설정할 필요가 없습니다. 행이 있는 테이블로 가져온 데이터로부터 기본 키 값을 업로드하고 기본 키가 충돌할 가능성이 있는 경우에만 `Ignoreduplicatekeys`를 `true`로 설정해야 합니다.  
  
  
