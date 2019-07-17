---
title: Updategrams (SQLXML 4.0)에서 데이터베이스 동시성 문제 처리 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <before> block
- low concurrency protection
- database concurrency [SQLXML]
- timestamp column [SQLXML]
- updategrams [SQLXML], database concurrency
- high concurrency protection [SQLXML]
- optimistic concurrency control
- concurrency [SQLXML]
- intermediate concurrency protection [SQLXML]
ms.assetid: d4b908d1-b25b-4ad9-8478-9cd882e8c44e
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cb7981be5bcb3885003e0fdd7adc367b28c9690c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086860"
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>Updategram의 데이터베이스 동시성 문제 처리(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  다른 데이터베이스 업데이트 메커니즘과 마찬가지로 updategram에서도 다중 사용자 환경에서 데이터의 동시 업데이트를 처리해야 합니다. Updategram은 선택한 필드 데이터의 스냅샷을 비교하는 방법으로 업데이트 대상 데이터를 데이터베이스에서 마지막으로 읽은 이후 다른 사용자 응용 프로그램에서 해당 데이터를 변경했는지 여부를 확인하는 낙관적 동시성 제어를 사용합니다. 이러한 스냅숏 값을 포함 하는 Updategrams는  **\<전에 >** 는 updategrams의 블록. 데이터베이스를 업데이트 하기 전에 updategram에 지정 된 값을 검사 하면  **\<전에 >** 업데이트가 유효한 지 확인 하기 위해 데이터베이스의 현재 값에 대 한 블록.  
  
 낙관적 동시성 제어는 updategram에 낮음(없음), 중간, 높음이라는 세 가지 보호 수준을 제공합니다. Updategram을 적절하게 지정하여 필요한 보호 수준을 결정할 수 있습니다.  
  
## <a name="lowest-level-of-protection"></a>가장 낮은 수준의 보호  
 이 보호 수준에서는 데이터베이스를 마지막으로 읽은 후 적용된 다른 업데이트에 대한 참조 없이 업데이트가 처리됩니다. 기본 키 열만 지정 하면 이러한 경우에는  **\<전에 >** 차단 된 레코드를 식별 하 고에서 업데이트 된 정보를 지정은  **\<후 >** 블록입니다.  
  
 예를 들어 다음 updategram에서 새 연락처 전화 번호는 이전 전화 번호가 무엇이었는지에 상관없이 올바른 전화 번호입니다. 통지 방법을  **\<전에 >** 블록에만 기본 키 열 (ContactID) 지정 합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="intermediate-level-of-protection"></a>중간 수준의 보호  
 이 보호 수준의 경우 updategram은 사용자의 트랜잭션에서 레코드를 읽은 후 다른 트랜잭션에서 값을 변경하지 않았는지 확인하기 위해 업데이트 대상 데이터의 현재 값을 데이터베이스 열의 값과 비교합니다.  
  
 업데이트 된 열 기본 키 열을 지정 하 여 이러한 수준의 보호를 얻을 수 있는  **\<전에 >** 블록.  
  
 예를 들어 다음 updategram은 ContactID가 1인 연락처의 Person.Contact 테이블의 Phone 열 값을 변경합니다. **\<전에 >** 블록 지정 된 **전화** 특성을 특성 값이 값이 업데이트를 적용 하기 전에 데이터베이스의 해당 열에 있는 값을 일치 하는지 확인 합니다. .  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" Phone="398-555-0132" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="high-level-of-protection"></a>높은 수준의 보호  
 높은 수준의 보호를 사용하면 응용 프로그램에서 레코드를 마지막으로 읽은 후 레코드가 동일하게 유지되는지 확인할 수 있습니다. 다시 말해 응용 프로그램에서 레코드를 읽은 후 다른 트랜잭션에 의해 해당 레코드가 변경되지 않았다는 것을 확인할 수 있습니다.  
  
 다음과 같은 두 가지 방법으로 동시 업데이트에 대해 이와 같은 높은 수준의 보호를 사용할 수 있습니다.  
  
-   테이블에 추가 열을 지정 하면  **\<전에 >** 블록.  
  
     추가 열을 지정 하는 경우는  **\<전에 >** updategram은 블록에 이러한 열이 업데이트를 적용 하기 전에 데이터베이스에 있던 값을 사용 하 여 지정 된 값을 비교 합니다. 트랜잭션에서 레코드를 읽은 후 레코드 열 중 하나라도 변경되었으면 updategram은 업데이트를 수행하지 않습니다.  
  
     예를 들어 다음 updategram shift 이름이 업데이트 되지만 (StartTime, EndTime) 열에 지정 된  **\<전에 >** 블록을 더 높은 수준의 동시에 대 한 보호를 요청 함으로써 업데이트합니다.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1"   
                 Name="Day"   
                 StartTime="1900-01-01 07:00:00.000"   
                 EndTime="1900-01-01 15:00:00.000" />  
    </updg:before>  
    <updg:after>  
       <HumanResources.Shift Name="Morning" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
     레코드의 모든 열 값을 지정 하 여 가장 높은 수준의 보호를 지정 하는이 예제는  **\<전에 >** 블록입니다.  
  
-   에 타임 스탬프 열 (있는 경우)를 지정 하면  **\<전에 >** 블록입니다.  
  
     모든 레코드 열을 지정 하는 대신 합니다  **\<하기 전에**> 블록 지정 해도 타임 스탬프 열 (테이블에 하나) 하는 경우에 기본 키 열과 함께  **\<하기 전에 >** 블록입니다. 데이터베이스는 레코드가 업데이트될 때마다 타임스탬프 열을 고유한 값으로 업데이트합니다. 이 경우 updategram은 타임스탬프 값을 데이터베이스의 해당 값과 비교합니다. 타임스탬프 값은 데이터베이스에 이진 값으로 저장되므로 따라서 스키마에서 타임 스탬프 열 지정 해야 합니다 **dt:type="bin.hex"** 를 **dt:type="bin.base64"** , 또는 **sql: datatype = "타임 스탬프"** 합니다. (지정할 수 있습니다 합니다 **xml** 데이터 형식 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다.)  
  
#### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  이 테이블을 만들 합니다 **tempdb** 데이터베이스:  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (  
                 CustomerID  varchar(5),  
                 ContactName varchar(20),  
                 LastUpdated timestamp)  
    ```  
  
2.  이 예제 레코드를 추가합니다.  
  
    ```  
    INSERT INTO Customer (CustomerID, ContactName) VALUES   
                         ('C1', 'Andrew Fuller')  
    ```  
  
3.  다음 XSD 스키마를 복사하여 메모장에 붙여넣고 ConcurrencySampleSchema.xml로 저장합니다.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Customer" sql:relation="Customer" >  
       <xsd:complexType>  
            <xsd:attribute name="CustomerID"    
                           sql:field="CustomerID"   
                           type="xsd:string" />   
  
            <xsd:attribute name="ContactName"    
                           sql:field="ContactName"   
                           type="xsd:string" />  
  
            <xsd:attribute name="LastUpdated"   
                           sql:field="LastUpdated"   
                           type="xsd:hexBinary"   
                 sql:datatype="timestamp" />  
  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
4.  다음 updategram 코드를 메모장에 복사한 다음 이전 단계에서 만든 스키마를 저장한 것과 같은 디렉터리에 ConcurrencySampleTemplate.xml로 저장합니다. 아래의 LastUpdated 타임스탬프 값은 Customer 테이블의 타임스탬프 값과 다르므로 테이블에서 LastUpdated의 실제 값을 복사하여 updategram에 붙여넣어야 합니다.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
    <updg:before>  
       <Customer CustomerID="C1"   
                 LastUpdated = "0x00000000000007D1" />  
    </updg:before>  
    <updg:after>  
       <Customer ContactName="Robert King" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
5.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="ContactName" />  
    <AttributeType name="LastUpdated"  dt:type="bin.hex"   
                                       sql:datatype="timestamp" />  
    <attribute type="CustomerID" />  
    <attribute type="ContactName" />  
    <attribute type="LastUpdated" />  
</ElementType>  
</Schema>  
```  
  
## <a name="see-also"></a>관련 항목  
 [Updategram 보안 고려 사항 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
