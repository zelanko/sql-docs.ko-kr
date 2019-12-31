---
title: XML 대량 로드에 대 한 지침 및 제한 사항 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ec3b70c4a37382bb3fa8641e4224750a4337c28d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246757"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>XML 대량 로드에 대한 지침 및 제한 사항(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 대량 로드를 사용하려면 다음의 지침과 제한 사항을 알아 두어야 합니다.  
  
-   인라인 스키마는 지원되지 않습니다.  
  
     원본 XML 문서에 인라인 스키마가 있는 경우 XML 대량 로드에서 해당 스키마를 무시합니다. XML 데이터 외부의 XML 대량 로드에 대한 매핑 스키마를 지정합니다. **Xmlns = "x:schema"** 특성을 사용 하 여 노드에서 매핑 스키마를 지정할 수 없습니다.  
  
-   XML 문서는 형식만 검사되고 유효성은 검사되지 않습니다.  
  
     Xml 대량 로드는 xml 문서를 검사 하 여 제대로 구성 되었는지 여부를 확인 합니다. 즉, XML이 World Wide Web 컨소시엄 XML 1.0 권장 사항의 구문 요구 사항을 준수 하는지 확인 합니다. 문서 형식이 올바르지 않으면 XML 대량 로드에서 처리가 취소되고 오류가 반환됩니다. 그러나 문서가 조각인 경우(예: 문서에 단일 루트 요소가 없는 경우)에만 예외적으로 형식이 올바르지 않은 문서도 로드됩니다.  
  
     XML 대량 로드는 XML 데이터 파일 안에 정의되거나 참조되는 XML 데이터 또는 DTD 스키마와 관련하여 문서의 유효성을 검사하지 않습니다. 또한 XML 대량 로드에서는 제공된 매핑 스키마를 기준으로 XML 데이터 파일의 유효성을 검사하지 않습니다.  
  
-   모든 XML 프롤로그 정보는 무시됩니다.  
  
     Xml 대량 로드는 XML 문서에서 \<루트> 요소 앞뒤의 모든 정보를 무시 합니다. 예를 들어 모든 XML 선언, 내부 DTD 정의, 외부 DTD 참조, 주석 등은 무시됩니다.  
  
-   두 테이블(예: Customer 테이블과 CustOrder 테이블) 간의 기본 키/외래 키 관계를 정의하는 매핑 스키마가 있는 경우, 스키마에서 기본 키가 들어 있는 테이블 설명이 먼저 나오고 외래 키 열이 들어 있는 테이블이 그 다음에 나와야 합니다. 그 이유는 스키마에서 테이블이 식별 되는 순서는 데이터베이스에 로드 하는 데 사용 되는 순서 이기 때문입니다. 예를 들어 다음 XDR 스키마는 ** \<Order>** 요소가 ** \<Customer>** 요소 보다 먼저 설명 되기 때문에 XML 대량 로드에서 사용 되는 경우 오류를 생성 합니다. 여기서 CustOrder의 CustomerID 열은 Cust 테이블의 CustomerID 기본 키 열을 참조하는 외래 키 열입니다.  
  
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
  
-   스키마가 **sql: 오버플로 필드** 주석을 사용 하 여 오버플로 열을 지정 하지 않는 경우 Xml 대량 로드는 xml 문서에 있는 모든 데이터를 무시 하지만 매핑 스키마에는 설명 되지 않습니다.  
  
     XML 대량 로드는 알려진 태그가 XML 데이터 스트림에서 발견될 때마다 사용자가 지정한 매핑 스키마를 적용합니다. 그러나 XML 문서에는 포함되었지만 스키마에 설명되지 않은 데이터는 무시합니다. 예를 들어 ** \<고객>** 요소를 설명 하는 매핑 스키마가 있다고 가정 합니다. XML 데이터 파일에는 모든 ** \<고객>** 요소를 포함 하는 ** \<allcustomers>** 루트 태그 (스키마에 설명 되어 있지 않음)가 있습니다.  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     이 경우 XML 대량 로드는 ** \<allcustomers>** 요소를 무시 하 고 ** \<Customer>** 요소에서 매핑을 시작 합니다. XML 대량 로드는 XML 문서에는 있지만 스키마에는 설명되어 있지 않은 모든 요소를 무시합니다.  
  
     ** \<Order>** 요소를 포함 하는 다른 XML 원본 데이터 파일을 고려 합니다. 이러한 요소는 매핑 스키마에 설명되어 있지 않습니다.  
  
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
  
     XML 대량 로드는 이러한 ** \<순서>** 요소를 무시 합니다. 그러나 스키마에서 **sql: 오버플로 필드**주석을 사용 하 여 열을 오버플로 열로 식별 하는 경우 XML 대량 로드는이 열에 사용 되지 않은 모든 데이터를 저장 합니다.  
  
-   CDATA 섹션과 엔터티 참조는 데이터베이스에 저장되기 전에 해당하는 문자열로 변환됩니다.  
  
     이 예에서 CDATA 섹션은 ** \<City>** 요소에 대 한 값을 래핑합니다. XML 대량 로드는 ** \<도시>** 요소를 데이터베이스에 삽입 하기 전에 문자열 값 (")을 추출 합니다.  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML 대량 로드는 엔터티 참조를 유지하지 않습니다.  
  
-   매핑 스키마에서 특성의 기본값을 지정하고 XML 원본 데이터에 해당 특성이 없으면, XML 대량 로드는 기본값을 사용합니다.  
  
     다음 샘플 XDR 스키마는 기본값을 **HireDate** 특성에 할당 합니다.  
  
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
  
     이 XML 데이터에서 **HireDate** 특성은 두 번째 ** \<고객>** 요소에 없습니다. XML 대량 로드는 두 번째 ** \<고객>** 요소를 데이터베이스에 삽입 하 고 스키마에 지정 된 기본값을 사용 합니다.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   **Sql: url 인코딩** 주석은 지원 되지 않습니다.  
  
     XML 데이터 입력에 URL을 지정하면 대량 로드는 해당 위치에서 데이터를 읽지 못합니다.  
  
     매핑 스키마에 식별된 테이블이 생성됩니다(데이터베이스가 존재해야 함). 하나 이상의 테이블이 데이터베이스에 이미 있는 경우 SGDropTables 속성은 이러한 기존 테이블을 삭제 하 고 다시 만들지 여부를 결정 합니다.  
  
-   SchemaGen 속성 (예: SchemaGen = true)을 지정 하면 매핑 스키마에서 식별 된 테이블이 생성 됩니다. 그러나 SchemaGen은 다음과 같은 한 가지 예외를 제외 하 고 이러한 테이블에 제약 조건 (예: PRIMARY KEY/FOREIGN KEY 제약 조건)을 만들지 않습니다. 관계의 기본 키를 구성 하는 XML 노드가 ID의 XML 유형 (즉, XSD의 경우 **type = "xsd: ID"** )으로 정의 되 고 SGUseID 속성이 True로 설정 된 경우에는 id로 형식화 된 노드에서 생성 되는 기본 키가 아니라 기본 키/외래 키 관계가 매핑 스키마 관계에서 생성 됩니다.  
  
-   SchemaGen은 XSD 스키마 패싯 및 확장을 사용 하 여 관계형 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 스키마를 생성 하지 않습니다.  
  
-   대량 로드에서 SchemaGen 속성 (예: SchemaGen = true)을 지정 하면 지정 된 테이블 (공유 이름의 뷰 아님)만 업데이트 됩니다.  
  
-   SchemaGen은 주석이 추가 된 XSD에서 관계형 스키마를 생성 하는 기본 기능만 제공 합니다. 필요한 경우 생성된 테이블을 사용자가 직접 수정해야 합니다.  
  
-   테이블 간에 둘 이상의 관계가 존재 하는 경우 SchemaGen은 두 테이블 간에 관련 된 모든 키를 포함 하는 단일 관계를 만들려고 시도 합니다. 이 제한 사항은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 오류의 원인이 될 수 있습니다.  
  
-   XML 데이터를 데이터베이스에 대량 로드할 경우 데이터베이스 열에 매핑되는 특성 또는 자식 요소가 매핑 스키마에 적어도 하나 있어야 합니다.  
  
-   XML 대량 로드를 사용하여 날짜 값을 삽입할 경우 값을 (-)CCYY-MM-DD((+-)TZ) 형식으로 지정해야 합니다. 이 형식은 날짜에 대한 표준 XSD 형식입니다.  
  
-   일부 속성 플래그는 다른 속성 플래그와 함께 사용할 수 없습니다. 예를 들어 대량 로드는 **Keepidentity = false**와 함께 **Ignoreduplicatekeys = true** 를 지원 하지 않습니다. **Keepidentity = false**인 경우 대량 로드는 서버에서 키 값을 생성 하는 것으로 예상 합니다. 테이블에는 키에 대 한 **IDENTITY** 제약 조건이 있어야 합니다. 서버에서는 중복 키를 생성 하지 않습니다. 즉, **Ignoreduplicatekeys** 를 **true**로 설정할 필요가 없습니다. 들어오는 데이터의 기본 키 값을 행이 있는 테이블로 업로드 하 고 기본 키 값이 충돌할 가능성이 있는 경우에만 **Ignoreduplicatekeys** 를 **true** 로 설정 해야 합니다.  
  
  
