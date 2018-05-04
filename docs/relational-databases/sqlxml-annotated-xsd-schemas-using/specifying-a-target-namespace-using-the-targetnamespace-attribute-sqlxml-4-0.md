---
title: 대상 Namespace를 사용 하 여 targetNamespace 특성 (SQLXML 4.0)를 지정 하 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- targetNamespace attribute
- XSD schemas [SQLXML], target namespaces
- annotated XSD schemas, target namespaces
- xsd:targetNamespace
- attributeFormDefault attribute
- elementFormDefault attribute
- target namespaces [SQLXML]
ms.assetid: f3df9877-6672-4444-8245-2670063c9310
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f66bb00ee4b1a40bdcbba3bf97dad1a0e1f8595f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>targetNamespace 특성을 사용하여 대상 네임스페이스 지정(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSD 스키마를 작성할에서 XSD를 사용할 수 있습니다 **targetNamespace** 특성 대상 네임 스페이스를 지정 합니다. 이 항목에서는 설명 어떻게 XSD **targetNamespace**, **elementFormDefault**, 및 **attributeFormDefault** 특성이 작동 되는 XML 인스턴스에 미치는 영향 생성 된 네임 스페이스와 XPath 쿼리를 지정 하는 방법 및 합니다.  
  
 사용할 수는 **xsd: targetnamespace** 을 기본 네임 스페이스의 요소와 특성을 다른 네임 스페이스에 배치할 특성입니다. 또한 로컬로 선언된 스키마 요소 및 특성을 접두사를 사용하여 명시적으로 또는 암시적으로(기본 설정) 네임스페이스에서 정규화된 것으로 표시할지 여부를 지정할 수도 있습니다. 사용할 수는 **elementFormDefault** 및 **attributeFormDefault** 특성은  **\<xsd: schema >** 전체적으로 지정 하는 요소는 로컬 요소 및 특성 또는 사용자의 자격을 사용할 수는 **양식** 특성을 개별 요소와 특성을 개별적으로 지정 합니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 참조 [SQLXML 예 실행에 대 한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-a-target-namespace"></a>1. 대상 네임스페이스 지정  
 사용 하 여 대상 네임 스페이스를 지정 하는 다음 XSD 스키마는 **xsd: targetnamespace** 특성입니다. 스키마도 설정 하는 **elementFormDefault** 및 **attributeFormDefault** 특성 값을 **"unqualified"** (이러한 특성에 대 한 기본값). 전역 선언 이며 모든 로컬 요소에 영향을 줍니다 (**\<순서 >** 스키마에서)와 특성 (**CustomerID**, **ContactName**, 및  **OrderID** 스키마에).  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:CO="urn:MyNamespace"   
            targetNamespace="urn:MyNamespace" >  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer"   
               sql:relation="Sales.Customer"   
               type="CO:CustomerType" />  
  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustOrders"  
                     type="CO:OrderType" />  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesPersonID"  type="xsd:string" />  
  </xsd:complexType>  
  <xsd:complexType name="OrderType" >  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 스키마에서 다음을 확인하십시오.  
  
-   **CustomerType** 및 **OrderType** 형식 선언은 전역, 따라서 스키마의 대상 네임 스페이스에 포함 됩니다. 이러한 종류의 선언에서 참조 되는 경우에 결과적으로,  **\<고객 >** 요소 및 해당  **\<순서 >** 자식 요소에 연결 된 접두사가 지정 됩니다 대상 네임 스페이스입니다.  
  
-   **\<고객 >** 스키마에서 전역 요소 이기 때문에 스키마의 대상 네임 스페이스에 요소도 포함 되어 있습니다.  
  
 스키마에 대해 다음 XPath 쿼리를 실행합니다.  
  
```  
(/CO:Customer[@CustomerID=1)   
```  
  
 이 XPath 쿼리를 실행하면 다음 인스턴스 문서가 생성됩니다. 여기에는 주문의 일부만 나와 있습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <y0:Customer xmlns:y0="urn:MyNamespace"   
      CustomerID="ALFKI" ContactName="Maria Anders">  
        <Order CustomerID="ALFKI" OrderID="10643" />   
        <Order CustomerID="ALFKI" OrderID="10692" />   
        ...  
  </y0:Customer>  
  </ROOT>  
```  
  
 이 인스턴스 문서 urn: MyNamespace 네임 스페이스를 정의 하 고 접두사 (y0)를을 연결 합니다. 접두사에만 적용 되는  **\<고객 >** 전역 요소입니다. (의 자식으로 선언 되어 있어이 요소는 전역  **\<xsd: schema >** 스키마의 요소입니다.)  
  
 때문에 로컬 요소 및 특성에는 접두사가 적용 되지 않습니다 값 **elementFormDefault** 및 **attributeFormDefault** 특성으로 설정 되어 **"unqualified"** 스키마에 있습니다. **\<순서 >** 요소는 해당 선언의 자식으로 표시 되기 때문에 로컬는  **\<complexType >** 정의 하는 요소는  **\< CustomerType >** 요소입니다. 마찬가지로, 해당 특성 (**CustomerID**, **OrderID**, 및 **ContactName**)은 로컬, 전역이 아니라 합니다.  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>이 스키마의 작업 예제를 만들려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 targetNameSpace.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 targetNamespace.xml을 저장한 디렉터리와 같은 디렉터리에 targetNameSpaceT.xml로 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="targetNamespace.xml"  
                       xmlns:CO="urn:MyNamespace" >  
        /CO:Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     템플릿의 XPath 쿼리에서 반환 된  **\<고객 >** CustomerID가 1 인 고객에 대 한 요소입니다. XPath 쿼리에서 요소에 대해서만 네임스페이스 접두사가 지정되고 특성에 대해서는 지정되지 않는 것을 알 수 있습니다. 스키마에 지정된 대로 로컬 특성이 정규화되지 않는 것입니다.  
  
     매핑 스키마(targetNamespace.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 참조 [SQLXML 쿼리 실행을 사용 하 여 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 스키마를 지정 하는 경우 **elementFormDefault** 및 **attributeFormDefault** 특성 값 **"qualified"**, 인스턴스 문서는 모든 로컬 적용 됩니다 특성과 해당 요소를 정규화합니다. 이러한 특성을 포함 하도록 앞의 스키마를 변경할 수는  **\<xsd: schema >** 요소 템플릿을 다시 실행 하십시오. 이 경우 특성이 인스턴스에서도 정규화되므로 네임스페이스 접두사를 포함하도록 XPath 쿼리가 변경됩니다.  
  
 수정된 XPath 쿼리는 다음과 같습니다.  
  
```  
/CO:Customer[@CO:CustomerID=1]  
```  
  
 반환되는 XML 문서는 다음과 같습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <y0:Customer xmlns:y0="urn:MyNamespace" CustomerID="1" SalesPersonID="280">  
      <Order SalesOrderID="43860" CustomerID="1" />   
      <Order SalesOrderID="44501" CustomerID="1" />   
      <Order SalesOrderID="45283" CustomerID="1" />   
      <Order SalesOrderID="46042" CustomerID="1" />   
   </y0:Customer>  
</ROOT>  
```  
  
  
