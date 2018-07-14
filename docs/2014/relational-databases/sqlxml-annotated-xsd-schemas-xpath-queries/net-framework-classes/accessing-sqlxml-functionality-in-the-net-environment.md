---
title: .NET 환경에서 SQLXML 기능 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], accessing SQLXML functionality
- SQLXML Managed Classes, accessing SQLXML functionality
- DiffGrams [SQLXML], accessing SQLXML functionality
- .NET Framework [SQLXML], accessing SQLXML functionality
ms.assetid: 74744535-2945-414d-9a5b-7e8cc363953a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 53a61e858eef876716c07ab54186178c4e4e202b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323813"
---
# <a name="accessing-sqlxml-functionality-in-the-net-environment"></a>.NET 환경에서 SQLXML 기능 액세스
  이 예에서는 다음 내용을 설명합니다.  
  
-   사용 하는 방법 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML Managed Classes (Microsoft.Data.SqlXml) Microsoft에 액세스 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 환경입니다.  
  
-   .NET Framework 환경에서 생성된 DiffGram이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 데이터 업데이트를 적용하는 방법  
  
 이 응용 프로그램에서는 XSD 스키마에 대해 XPath 쿼리를 실행합니다. 연락처 데이터를 XML 문서를 반환 하는 XPath 쿼리 실행 (**FirstName**하십시오 **LastName**). 응용 프로그램은 .NET Framework 환경의 데이터 집합에 XML 문서를 로드합니다. 그런 다음 데이터 집합에 있는 첫 번째 연락처에서 이름을 "Susan"으로 변경합니다. 그리고 해당 데이터 집합에서 DiffGram을 생성하며, 이 DiffGram에 지정된 업데이트(직원 이름에 대한 변경 내용)를 Person.Contact 테이블에 적용합니다.  
  
> [!NOTE]  
>  코드에서 연결 문자열에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정해야 합니다.  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      DataRow row;  
      SqlXmlAdapter ad;  
      //need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandText = "Con";  
      cmd.CommandType = SqlXmlCommandType.XPath;  
      cmd.SchemaPath = "MySchema.xml";  
      //load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      row = ds.Tables["Con"].Rows[0];  
      row["FName"] = "Susan";  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
 **예제를 테스트 합니다.**  
  
 이 예를 테스트하려면 컴퓨터에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework가 설치되어 있어야 합니다.  
  
1.  이 XSD 스키마(MySchema.xml)를 폴더에 저장합니다.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Con" sql:relation="Person.Contact" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="FName"    
                         sql:field="FirstName"   
                         type="xsd:string" />   
            <xsd:element name="LName"    
                         sql:field="LastName"    
                         type="xsd:string" />  
         </xsd:sequence>  
         <xsd:attribute name="ContactID" type="xsd:integer" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
2.  이 예에서 제공하는 C# 코드(DocSample.cs)를 스키마가 저장된 폴더와 같은 폴더에 저장합니다. (다른 폴더에 파일을 저장하는 경우 코드를 편집하여 매핑 스키마에 대해 적합한 디렉터리 경로를 지정해야 합니다.)  
  
3.  코드를 컴파일합니다. 다음을 사용하여 명령 프롬프트에서 코드를 컴파일합니다.  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     이렇게 하면 실행 파일(DocSample.exe)이 만들어집니다.  
  
 명령 프롬프트에서 DocSample.exe를 실행합니다.  
  
  
