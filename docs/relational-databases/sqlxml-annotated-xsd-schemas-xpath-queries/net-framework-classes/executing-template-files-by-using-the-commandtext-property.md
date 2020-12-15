---
title: CommandText 속성을 사용 하 여 템플릿 파일 실행
description: SQLXML CommandText 속성을 사용 하 여 SQL 또는 XPath 쿼리를 포함 하는 템플릿 파일의 이름을 지정 하는 방법의 예를 보여 줍니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], executing template files
- SQLXML Managed Classes, executing template files
- templates [SQLXML], SQLXML Managed Classes
- executing template files [SQLXML]
- CommandText property
ms.assetid: f1b1278d-252d-4a06-836e-4ef77f338ef9
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 86cf0f5133adf3bbf1e8efa8ff0e93ff4bc98c66
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414299"
---
# <a name="executing-template-files-by-using-the-commandtext-property"></a>CommandText 속성을 사용하여 템플릿 파일 실행
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  이 예에서는 CommandText 속성을 사용 하 여 SQL 또는 XPath 쿼리로 구성 된 템플릿 파일을 지정할 수 있는 방법을 보여 줍니다. SQL 또는 XPath 쿼리를 CommandText 값으로 지정 하는 대신 파일 이름을 값으로 지정할 수 있습니다. 다음 예제에서 CommandType 속성은 SqlXmlCommandType. 템플릿 파일로 지정 됩니다.  
  
 예제 애플리케이션에서 이 템플릿을 실행합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
    SELECT TOP 2 ContactID, FirstName, LastName   
    FROM   Person.Contact  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 이 애플리케이션은 C# 예제 애플리케이션입니다. 따라서 애플리케이션을 테스트하려면 템플릿(TemplateFile.xml)을 저장한 다음 애플리케이션을 실행해야 합니다.  
  
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
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandType = SqlXmlCommandType.TemplateFile;  
         cmd.CommandText = "TemplateFile.xml";  
         using (Stream strm = cmd.ExecuteStream()){  
            using (StreamReader sr = new StreamReader(strm)){  
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
  
### <a name="to-test-the-application"></a>애플리케이션을 테스트하려면  
  
1.  컴퓨터에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework가 설치되어 있는지 확인합니다.  
  
2.  이 예에서 제공하는 XML 템플릿(TemplateFile.xml)을 폴더에 저장합니다.  
  
3.  이 예에서 제공하는 C# 코드(DocSample.cs)를 스키마가 저장된 폴더와 같은 폴더에 저장합니다. (다른 폴더에 파일을 저장하는 경우 코드를 편집하여 매핑 스키마에 대해 적합한 디렉터리 경로를 지정해야 합니다.)  
  
4.  코드를 컴파일합니다. 다음을 사용하여 명령 프롬프트에서 코드를 컴파일합니다.  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     이렇게 하면 실행 파일(DocSample.exe)이 만들어집니다.  
  
5.  명령 프롬프트에서 DocSample.exe를 실행합니다.  

 템플릿에 매개 변수를 전달 하는 경우 매개 변수 이름은 at 기호 (@)로 시작 해야 합니다. 예를 들어 p.Name = " \@ ContactID"입니다. 여기서 p는 SqlXmlParameter 개체입니다.  
  
 다음은 하나의 매개 변수를 사용하는 업데이트된 템플릿입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:header>  
     <sql:param name='ContactID'>1</sql:param>    
  </sql:header>  
  <sql:query>  
    SELECT ContactID, FirstName, LastName  
    FROM   Person.Contact  
    WHERE  ContactID=@ContactID  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 다음은 템플릿을 실행하기 위해 매개 변수가 전달되는 업데이트된 코드입니다.  
  
```  
public static int testParams()  
{  
  
   Stream strm;  
   SqlXmlParameter p;  
  
   SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
   cmd.CommandType = SqlXmlCommandType.TemplateFile;  
   cmd.CommandText = "TemplateFile.xml";  
   p = cmd.CreateParameter();  
   p.Name="@ContactID";  
   p.Value = "1";  
   strm = cmd.ExecuteStream();  
   StreamReader sw = new StreamReader(strm);  
   Console.WriteLine(sw.ReadToEnd());  
   return 0;        
}  
```  
  
  
