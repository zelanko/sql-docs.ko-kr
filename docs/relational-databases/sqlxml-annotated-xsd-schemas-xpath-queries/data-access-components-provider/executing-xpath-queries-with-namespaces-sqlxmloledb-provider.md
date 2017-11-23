---
title: "네임 스페이스 (SQLXMLOLEDB 공급자)와 XPath 쿼리 실행 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- SQLXMLOLEDB Provider, executing XPath queries
- namespaces property
- queries [SQLXML], SQLXMLOLEDB Provider
- XPath queries [SQLXML], namespaces
- XPath queries [SQLXML], SQLXMLOLEDB Provider
- namespaces [SQLXML], XPath queries
ms.assetid: 024a4b7d-435d-47ba-9e80-2c2f640108f5
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1ce8d6b1a7a3d828112841bfcaa71921bfb215d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="executing-xpath-queries-with-namespaces-sqlxmloledb-provider"></a>네임스페이스가 있는 XPath 쿼리 실행(SQLXMLOLEDB 공급자)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]XPath 쿼리는 네임 스페이스를 포함할 수 있습니다. 스키마 요소의 네임스페이스가 한정된 경우 즉, 스키마 요소에 대상 네임스페이스가 포함된 경우 스키마에 대한 XPath 쿼리에서 이 네임스페이스를 지정해야 합니다.  
  
 SQLXML 4.0에서는 와일드카드 문자(*)를 사용할 수 없으므로 네임스페이스 접두사를 사용하여 XPath 쿼리를 지정해야 합니다. 이 접두사를 해결 하려면 네임 스페이스 바인딩을 지정 하려면 네임 스페이스 속성을 사용 합니다.  
  
 다음 예제에서는 XPath 쿼리에 와일드 카드 문자를 사용 하 여 네임 스페이스를 지정 (\*) local-name () 및 namespace-uri () XPath 함수입니다. 이 XPath 쿼리는 로컬 이름 여기서은 요소를 모두 반환 **연락처** 및 네임 스페이스 URI가 **urn: myschema:Contacts**합니다.  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 SQLXML 4.0에서는 이 XPath 쿼리를 네임스페이스 접두사를 사용하여 지정해야 합니다. 예로 **x: 연락처**여기서 **x** 네임 스페이스 접두사입니다. 다음과 같은 XSD 스키마를 살펴보십시오.  
  
```  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:con="urn:myschema:Contacts"  
            targetNamespace="urn:myschema:Contacts">  
<complexType name="ContactType">  
  <attribute name="CID" sql:field="ContactID" type="ID"/>  
  <attribute name="FName" sql:field="FirstName" type="string"/>  
  <attribute name="LName" sql:field="LastName"/>   
</complexType>  
<element name="Contact" type="con:ContactType" sql:relation="Person.Contact"/>  
</schema>  
```  
  
 이 스키마에서는 대상 네임스페이스를 정의하므로 스키마에 대한 XPath 쿼리(예: "Employee")에 네임스페이스가 포함되어 있어야 합니다.  
  
 다음은 앞의 XSD 스키마에 대한 XPath 쿼리(x:Employee)를 실행하는 예제 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 응용 프로그램입니다. 접두사를 해결 하려면 네임 스페이스 바인딩이 네임 스페이스 속성을 사용 하 여 지정 됩니다.  
  
> [!NOTE]  
>  코드에서 연결 문자열에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정해야 합니다. 또한 이 예에서는 데이터 공급자에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client(SQLNCLI11)를 사용하도록 지정하는데, 이렇게 하려면 추가 네트워크 클라이언트를 설치해야 합니다. 자세한 내용은 참조 [SQL Server Native Client에 대 한 시스템 요구 사항](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)합니다.  
  
```  
Option Explicit  
Private Sub Form_Load()  
    Dim con As New ADODB.Connection  
    Dim cmd As New ADODB.Command  
    Dim stm As New ADODB.Stream  
    con.Open "provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
    Set cmd.ActiveConnection = con  
    stm.Open  
    cmd.Properties("Output Stream").Value = stm  
    cmd.Properties("Output Encoding") = "utf-8"  
    cmd.Properties("Mapping schema") = "C:\DirectoryPath\con-ex.xml"  
    cmd.Properties("namespaces") = "xmlns:x='urn:myschema:Contacts'"  
    '  Debug.Print "Set Command Dialect to DBGUID_XPATH"  
    cmd.Dialect = "{ec2a4293-e898-11d2-b1b7-00c04f680c56}"  
    cmd.CommandText = "x:Contact"  
    cmd.Execute , , adExecuteStream   
    stm.Position = 0  
    Debug.Print stm.ReadText(adReadAll)  
End Sub  
```  
  
### <a name="to-test-this-application"></a>이 응용 프로그램을 테스트하려면  
  
1.  예제 XSD 스키마를 폴더에 저장합니다.  
  
2.  Visual Basic 실행 프로젝트를 만들고 여기로 코드를 복사합니다. 지정된 디렉터리 경로를 적절하게 변경합니다.  
  
3.  다음 프로젝트 참조를 추가합니다.  
  
    ```  
    "Microsoft ActiveX Data Objects 2.8 Library"  
    ```  
  
4.  응용 프로그램을 실행합니다.  
  
 다음은 결과의 일부입니다.  
  
```  
<y0:Employee xmlns:y0="urn:myschema:Contacts"   
             LName="Achong" CID="1" FName="Gustavo"/>  
<y0:Employee xmlns:y0="urn:myschema:Employees"   
             LName="Abel" CID="2" FName="Catherine"/>  
```  
  
 XML 문서에서 생성되는 접두사는 임의적이지만 동일한 네임스페이스에 매핑됩니다.  
  
  
