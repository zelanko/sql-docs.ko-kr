---
title: (SQLXML 4.0) Updategram 소개 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- updategrams [SQLXML], mapping schema specifying
- namespaces [SQLXML]
- updategrams [SQLXML], about updategrams
- attribute-centric mapping
- invalid characters [SQLXML]
- element-centric mapping [SQLXML]
- mapping schema [SQLXML], updategrams
- namespaces [SQLXML], updategrams
- executing updategrams [SQLXML]
- implicit schema mapping
ms.assetid: cfe24e82-a645-4f93-ab16-39c21f90cce6
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6c3d51e64669f2410ca6e99926734b767dba1f45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32973078"
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Updategram 소개(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  수정할 수 있습니다 (삽입, 업데이트 또는 삭제)에서 데이터베이스 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] updategram 이나 OPENXML을 사용 하 여 문서에서 기존 XML [!INCLUDE[tsql](../../../includes/tsql-md.md)] 함수입니다.  
  
 OPENXML 함수는 기존 XML 문서를 조각화하여 INSERT, UPDATE 또는 DELETE 문에 전달할 수 있는 행 집합을 제공함으로써 데이터베이스를 수정합니다. OPENXML을 사용하면 작업이 데이터베이스 테이블에 대해 직접 수행되기 때문에 OPENXML은 테이블과 같은 행 집합 공급자를 원본으로 표시할 수 있는 경우에 가장 적합합니다.  
  
 OPENXML과 마찬가지로 updategram을 사용하면 데이터베이스에서 데이터를 삽입, 업데이트 또는 삭제할 수 있습니다. 그러나 updategram은 주석 XSD(또는 XDR) 스키마에서 제공하는 XML 뷰에 대해 작업을 수행합니다. 예를 들면 매핑 스키마에서 제공하는 XML 뷰에 업데이트가 적용됩니다. 매핑 스키마에는 XML 요소와 특성을 해당 데이터베이스 테이블과 열에 매핑하는 데 필요한 정보가 있으며 updategram은 이 매핑 정보를 사용하여 데이터베이스 테이블과 열을 업데이트합니다.  
  
> [!NOTE]  
>  이 설명서에서는 사용자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 템플릿 및 매핑 스키마 지원에 대해 잘 알고 있다고 가정합니다. 자세한 내용은 참조 [주석이 추가 된 XSD 스키마 & #40; 소개 SQLXML 4.0 & #41; ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). XDR을 사용 하는 레거시 응용 프로그램에 대 한 참조 [주석이 추가 된 XDR 스키마 &#40;SQLXML 4.0에서 더 이상 사용&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)합니다.  
  
## <a name="required-namespaces-in-the-updategram"></a>Updategram의 필수 네임스페이스  
 Updategram에서 키워드와 같은  **\<동기화 >**,  **\<하기 전에 >**, 및  **\<후 >** 는 에 **:-microsoft-com:xml-updategram** 네임 스페이스입니다. 임의의 네임스페이스 접두사를 사용합니다. 이 설명서에는 **updg** 접두사 나타냅니다는 **updategram** 네임 스페이스입니다.  
  
## <a name="reviewing-syntax"></a>구문 검토  
 Updategram은 있는 템플릿이  **\<동기화 >**,  **\<하기 전에 >**, 및  **\<후 >** 블록의 구문을 구성 하는 updategram입니다. 다음 코드에서는 가장 간단한 형태의 updategram 구문을 보여 줍니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema= "AnnotatedSchemaFile.xml"] >  
    <updg:before>  
        ...  
    </updg:before>  
    <updg:after>  
        ...  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 다음 정의는 각 블록의 역할에 대해 설명합니다.  
  
 **\<before>**  
 레코드 인스턴스의 기존 상태("이전 상태"라고도 함)를 식별합니다.  
  
 **\<after>**  
 데이터가 변경될 새 상태를 식별합니다.  
  
 **\<sync>**  
 포함 된  **\<하기 전에 >** 및  **\<후 >** 블록입니다. A  **\<동기화 >** 블록 집합이 여러 개 포함할 수 있습니다  **\<하기 전에 >** 및  **\<후 >** 블록입니다. 둘 이상의 집합이 있으면  **\<하기 전에 >** 및  **\<후 >** 블록, 이러한 블록 (도 비어 있는 경우) 해야 쌍으로 지정 합니다. 또한 updategram 둘 이상 있을 수  **\<동기화 >** 블록입니다. 각  **\<동기화 >** 블록은 하나의 트랜잭션 단위 (즉의 모든 요소가  **\<동기화 >** 블록은 완료 되거나 아무 요소도 처리). 여러 개 지정 하는 경우  **\<동기화 >** 하나에 오류가 updategram에 블록  **\<동기화 >** 블록 다른 레코드에 영향을 주지는 않습니다  **\<동기화 >** 블록입니다.  
  
 내용에 따라 달라 집니다 updategram를 삭제, 삽입 또는 업데이트은 레코드 인스턴스가 있는지 여부는  **\<하기 전에 >** 및  **\<후 >** 블록:  
  
-   레코드 인스턴스가만 나타나고는  **\<하기 전에 >** 블록에서 해당 인스턴스가 없으면는  **\<후 >** 블록에 updategram 삭제 작업을 수행 합니다.  
  
-   레코드 인스턴스가만 나타나고는  **\<후 >** 블록에서 해당 인스턴스가 없으면는  **\<하기 전에 >** 블록은 삽입 작업입니다.  
  
-   레코드 인스턴스가 표시 되는  **\<하기 전에 >** 해당 인스턴스를 포함 하 고 차단는  **\<후 >** 블록은 업데이트 작업 합니다. Updategram에 지정 된 값으로 레코드 인스턴스를 업데이트 하는 경우에  **\<후 >** 블록입니다.  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>Updategram에 매핑 스키마 지정  
 Updategram에는 매핑 스키마(XSD 및 XDR 스키마 모두 지원됨)에서 제공하는 XML 추상화를 암시적 또는 명시적으로 지정할 수 있습니다. 즉, updategram은 매핑 스키마가 지정되었는지 여부에 관계없이 작업을 수행할 수 있습니다. 매핑 스키마를 지정 하지 않으면 updategram는 암시적 매핑 (기본 매핑) 가정, 여기서 각 요소에는  **\<하기 전에 >** 블록 또는  **\<후 >** 블록 테이블과 각 요소의 자식 요소에 매핑하거나 특성 데이터베이스의 열에 매핑됩니다. 매핑 스키마를 명시적으로 지정할 경우에는 updategram의 요소 및 특성이 매핑 스키마의 요소 및 특성과 일치해야 합니다.  
  
### <a name="implicit-default-mapping"></a>암시적(기본) 매핑  
 일반적으로 간단한 업데이트를 수행하는 updategram에는 매핑 스키마가 필요하지 않습니다. 이 경우에는 기본 매핑 스키마가 사용됩니다.  
  
 다음 updategram은 암시적 매핑을 보여 줍니다. 이 예에서 updategram은 Sales.Customer 테이블에 새 고객을 추가합니다. 이 updategram은 암시적 매핑을 사용 하기 때문에 \<Sales.Customer > 요소는 Sales.Customer 테이블에 매핑되고 CustomerID 및 SalesPersonID 특성은 Sales.Customer 테이블의 해당 열에 매핑됩니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
</updg:before>  
<updg:after>  
    <Sales.Customer CustomerID="1" SalesPersonID="277" />  
    </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="explicit-mapping"></a>명시적 매핑  
 매핑 스키마(XSD 또는 XDR)를 지정하면 updategram은 이 스키마를 사용하여 업데이트할 대상 데이터베이스 테이블과 열을 결정합니다.  
  
 매핑 스키마를 사용 하 여 명시적으로 제공 해야 updategram으로 복잡 한 업데이트 (예를 들어 매핑 스키마에 지정 된 부모-자식 관계를 기반으로 여러 테이블의 삽입 레코드)을 수행 하는 경우는  **매핑 스키마** updategram를 실행 하는 특성입니다.  
  
 Updategram은 템플릿이기 때문에 updategram의 매핑 스키마에 대해 지정된 경로는 템플릿 파일의 위치(updategram이 저장된 위치)를 기준으로 합니다. 자세한 내용은 참조 [Updategram에 주석이 추가 된 매핑 스키마 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)합니다.  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Updategram의 요소 중심 및 특성 중심 매핑  
 Updategram에 매핑 스키마가 지정되지 않은 기본 매핑의 경우 updategram 요소는 테이블에 매핑되고 자식 요소(요소 중심 매핑)와 특성(특성 중심 매핑)은 열에 매핑됩니다.  
  
### <a name="element-centric-mapping"></a>요소 중심 매핑  
 요소 중심 updategram의 경우 요소에는 요소의 속성을 나타내는 자식 요소가 포함됩니다. 한 가지 예로 다음 updategram을 참조하십시오. **\<Person.Contact >** 요소에 포함 된  **\<FirstName >** 및  **\<LastName >** 자식 요소입니다. 이러한 자식 요소는 속성의는  **\<Person.Contact >** 요소입니다.  
  
 Updategram은 암시적 매핑을 사용 하 여이 updategram은 매핑 스키마를 지정 하지 않으므로, 여기서는  **\<Person.Contact >** 요소 Person.Contact 테이블에 매핑되고 자식 요소가 매핑되는 FirstName로 및 LastName 열입니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:after>  
    <Person.Contact>  
       <FirstName>Catherine</FirstName>  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="attribute-centric-mapping"></a>특성 중심 매핑  
 특성 중심 매핑에서는 요소가 특성을 포함합니다. 다음 updategram은 특성 중심 매핑을 사용합니다. 이 예제는  **\<Person.Contact >** 요소는 **FirstName** 및 **LastName** 특성입니다. 이러한 특성의 속성은는  **\<Person.Contact >** 요소입니다. 이전 예제와 같이이 updategram은 매핑 스키마가 지정 되지 이므로 매핑할 암시적 매핑을 사용 하 여는  **\<Person.Contact >** Person.Contact 테이블에 매핑되고 요소의 특성을 요소는 테이블의 각 열입니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" LastName="Abel" />  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="using-both-element-centric-and-attribute-centric-mapping"></a>요소 중심 및 특성 중심 매핑 모두 사용  
 다음 updategram과 같이 요소 중심 및 특성 중심 매핑을 혼합하여 지정할 수 있습니다. 에  **\<Person.Contact >** 요소는 특성 및 자식 요소가 모두 포함 합니다. 또한 이 updategram에는 암시적 매핑이 사용됩니다. 따라서는 **FirstName** 특성 및  **\<LastName >** 자식 요소는 Person.Contact 테이블의 해당 열에 매핑됩니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" >  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="working-with-characters-valid-in-sql-server-but-not-valid-in-xml"></a>SQL Server에서는 유효하지만 XML에서는 유효하지 않은 문자 사용  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 테이블 이름에 공백이 포함될 수 있지만 이러한 형식의 테이블 이름은 XML에서는 유효하지 않습니다.  
  
 사용할 수 있는 문자를 인코딩하 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 식별자 하지는 않지만 유효한 XML 식별자를 사용 하 여 ' __xHHHH\_\_' 여기서 HHHH는 나타냅니다는 대부분 문자에 대 한 4 자리 16 진수 ucs-2 코드에 대 한 인코딩 값으로 중요 한 비트 우선 순서입니다. 이 인코딩 체계를 사용 하 여 공백 문자가 x0020 (4 자리 16 진수 코드에 나오는 공백 문자에 대 한);으로 대체 가져옵니다. 따라서 테이블 이름 [Order Details] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] _x005B_Order_x0020_Details_x005D 되\_ xml에서입니다.  
  
 와 같이 세 부분으로 구성 요소 이름을 지정 해야 하는 마찬가지로, \<[database]. [ owner]입니다. [table] >입니다. 으로 지정 해야 대괄호 문자 ([및]) XML에서 유효 하지 않으므로, 하므로 \<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_> 여기서 _x005B\_ 되는 왼쪽된 대괄호 () 문자와 _x005D에 대 한 인코딩을\_ 오른쪽 대괄호 (])에 대 한 인코딩입니다.  
  
## <a name="executing-updategrams"></a>Updategram 실행  
 Updategram은 템플릿이기 때문에 템플릿의 모든 처리 메커니즘이 적용됩니다. SQLXML 4.0에서는 다음 방법 중 하나로 updategram을 실행할 수 있습니다.  
  
-   ADO 명령으로 전송  
  
-   OLE DB 명령으로 전송  
  
## <a name="see-also"></a>관련 항목:  
 [Updategram 보안 고려 사항 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
