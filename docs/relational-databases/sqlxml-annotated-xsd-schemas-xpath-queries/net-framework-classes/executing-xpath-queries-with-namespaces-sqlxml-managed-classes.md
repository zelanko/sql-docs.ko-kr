---
title: 네임 스페이스를 사용 하 여 XPath 쿼리 실행 (SQLXML 관리 되는 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces property
- XPath queries [SQLXML], SQLXML Managed Classes
- queries [SQLXML], SQLXML Managed Classes
- XPath queries [SQLXML], namespaces
- Managed Classes [SQLXML], executing XPath queries
- SQLXML Managed Classes, executing XPath queries
- namespaces [SQLXML], XPath queries
ms.assetid: c6fc46d8-6b42-4992-a8f1-a8d4b8886e6e
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ee8abb015ab4dab9606c7f81cb86f712bf23ec54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785163"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxml-managed-classes"></a>네임스페이스가 포함된 XPath 쿼리 실행(SQLXML 관리되는 클래스)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XPath 쿼리에는 네임스페이스가 포함될 수 있습니다. 스키마 요소가 네임스페이스로 한정된 경우 즉, 스키마 요소에서 대상 네임스페이스를 사용하는 경우 스키마에 대한 XPath 쿼리에서 해당 네임스페이스를 지정해야 합니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0에서는 와일드카드 문자(*)를 사용할 수 없으므로 네임스페이스 접두사를 사용하여 XPath 쿼리를 지정해야 합니다. 접두사를 확인 하려면 네임 스페이스 바인딩을 지정 하는 네임 스페이스 속성을 사용 합니다.  
  
 다음 예의 XPath 쿼리 와일드 카드 문자를 사용 하 여 네임 스페이스를 지정 (\*) local-name () 및 namespace-uri () XPath 함수입니다. 이 XPath 쿼리는 로컬 이름이 인 요소를 모두 반환 **직원** URI는 네임 스페이스 **urn: myschema:Contacts**:  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 SQLXML 4.0에서는 네임스페이스 접두사를 사용하여 이 XPath 쿼리를 지정합니다. 예로 **x: 연락처**, 여기서 **x** 네임 스페이스 접두사입니다. 다음과 같은 XSD 스키마를 살펴보십시오.  
  
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
  
 이 스키마에서는 대상 네임스페이스를 정의하므로 이 스키마에 대한 XPath 쿼리(예: "Employee")에는 네임스페이스가 포함되어야 합니다.  
  
 다음 C# 예제 응용 프로그램은 위의 XSD 스키마(MySchema.xml)에 대해 XPath 쿼리를 실행합니다. 접두사를 해결 하려면 SqlXmlCommand 개체의 네임 스페이스 속성을 사용 하 여 네임 스페이스 바인딩을 지정 합니다.  
  
> [!NOTE]  
>  코드에서 연결 문자열에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정해야 합니다.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testXPath()  
      {  
         //Stream strm;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandText = "x:Contact[@CID='1']";  
         cmd.CommandType = SqlXmlCommandType.XPath;  
         cmd.RootTag = "ROOT";  
         cmd.Namespaces = "xmlns:x='urn:myschema:Contacts'";  
         cmd.SchemaPath = "MySchema.xml";  
         using (Stream strm = cmd.ExecuteStream()){  
            using (StreamReader sr = new StreamReader(strm)){  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
      public static int Main(String[] args)  
      {  
         testXPath();  
         return 0;  
      }  
   }  
```  
  
 이 예를 테스트하려면 컴퓨터에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework가 설치되어 있어야 합니다.  
  
### <a name="to-test-the-application"></a>응용 프로그램을 테스트하려면  
  
1.  이 예에서 제공하는 XSD 스키마(MySchema.xml)를 폴더에 저장합니다.  
  
2.  이 예에서 제공하는 C# 코드(DocSample.cs)를 스키마가 저장된 폴더와 같은 폴더에 저장합니다. (다른 폴더에 파일을 저장하는 경우 코드를 편집하여 매핑 스키마에 대해 적합한 디렉터리 경로를 지정해야 합니다.)  
  
3.  코드를 컴파일합니다. 다음을 사용하여 명령 프롬프트에서 코드를 컴파일합니다.  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     이렇게 하면 실행 파일(DocSample.exe)이 만들어집니다.  
  
4.  명령 프롬프트에서 DocSample.exe를 실행합니다.  
  
  
