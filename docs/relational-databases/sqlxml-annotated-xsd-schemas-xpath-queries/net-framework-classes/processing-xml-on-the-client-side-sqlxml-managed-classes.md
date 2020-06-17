---
title: 클라이언트 쪽에서 XML 처리 (SQLXML)
description: SQLXML 관리 되는 클래스에 있는 SqlXmlCommand 개체의 Clientside Xml 속성을 사용 하 여 클라이언트 쪽에서 XML을 처리 하는 방법에 대해 알아봅니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- processing XML on client side [SQLXML]
- client-side XML formatting
- Managed Classes [SQLXML], client-side XML formatting
- SQLXML Managed Classes, client-side XML formatting
- ClientSideXml property
ms.assetid: 5e7ecf18-66fc-49ff-bc50-83635cd7ac0b
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0dca939b5d3180e3a0d61b94797610b44344a73a
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84884237"
---
# <a name="processing-xml-on-the-client-side-sqlxml-managed-classes"></a>클라이언트 쪽에서 XML 처리(SQLXML 관리되는 클래스)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 예에서는 ClientSideXml 속성을 사용 하는 방법을 보여 줍니다. 애플리케이션은 서버에서 저장 프로시저를 실행합니다. 클라이언트 쪽에서 저장 프로시저의 결과(두 개의 열로 이루어진 행 집합)가 처리되어 XML 문서를 생성합니다.  
  
 다음 GetContacts 저장 프로시저는 AdventureWorks 데이터베이스의 Person. Contact 테이블에서 **FirstName** 및 **LastName** 을 반환 합니다.  
  
```  
USE AdventureWorks  
CREATE PROCEDURE GetContacts @LastName varchar(20)  
AS  
SELECT FirstName, LastName  
FROM   Person.Contact  
WHERE LastName = @LastName  
Go  
```  
  
 이 c # 응용 프로그램은 저장 프로시저를 실행 하 고 CommandText 값을 지정할 때 FOR XML AUTO 옵션을 지정 합니다. 응용 프로그램에서 SqlXmlCommand 개체의 ClientSideXml 속성이 true로 설정 됩니다. 이렇게 하면 행 집합을 반환하고 클라이언트에서 해당 행 집합에 XML 변환을 적용하는 기존 저장 프로시저를 실행할 수 있습니다.  
  
> [!NOTE]  
>  코드에서 연결 문자열에 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정해야 합니다.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
    static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         //Stream strm;  
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.ClientSideXml = true;  
         cmd.CommandText = "EXEC GetContacts ? FOR XML NESTED";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         using (Stream strm = cmd.ExecuteStream())   
         {  
            using (StreamReader sr = new StreamReader(strm))  
                  {  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
  
public static int Main(String[] args)  
{  
    testParams();  
    return 0;  
}  
}  
```  
  
 이 예를 테스트하려면 컴퓨터에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework가 설치되어 있어야 합니다.  
  
### <a name="to-test-the-application"></a>애플리케이션을 테스트하려면  
  
1.  저장 프로시저를 만듭니다.  
  
2.  이 예에 제공된 C# 코드(DocSample.cs)를 폴더에 저장합니다. 코드를 편집하여 적절한 로그인 및 암호 정보를 지정합니다.  
  
3.  코드를 컴파일합니다. 다음을 사용하여 명령 프롬프트에서 코드를 컴파일합니다.  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     이렇게 하면 실행 파일(DocSample.exe)이 만들어집니다.  
  
4.  명령 프롬프트에서 DocSample.exe를 실행합니다.  

