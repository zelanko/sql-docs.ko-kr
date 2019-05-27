---
title: CommandStream 속성을 사용 하 여 템플릿 파일 실행 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], executing template files
- SQLXML Managed Classes, executing template files
- templates [SQLXML], SQLXML Managed Classes
- CommandStream property
ms.assetid: 55c564e3-56d1-4d85-bcaa-703e2905dd57
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f0d753c7e56f4ae90a2b156ee8d521518d0029a
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010907"
---
# <a name="executing-template-files-by-using-the-commandstream-property"></a>CommandStream 속성을 사용하여 템플릿 파일 실행
  이 예제에서는 SqlXmlCommand 개체의 CommandStream 속성을 사용 하 여 SQL 또는 XPath 쿼리로 이루어진 템플릿 파일을 지정할 수 있습니다 하는 방법을 보여 줍니다. 이 응용 프로그램에는 FileStreamobject 명령 파일에 대해 열리고 파일 스트림은 실행 되는 CommandStream으로 할당 됩니다.  
  
 다음 예제에서는 CommandType 속성 SqlXmlCommandType.Template (아니라, TemplateFile)으로 지정 됩니다.  
  
 예제 XML 템플릿은 다음과 같습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
    SELECT TOP 2 ContactID, FirstName, LastName   
    FROM   Person.Contact  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 이것은 예제 C# 응용 프로그램입니다. 따라서 응용 프로그램을 테스트하려면 템플릿(TemplateFile.xml)을 저장한 다음 응용 프로그램을 실행해야 합니다. 응용 프로그램은 XML 템플릿에 지정된 쿼리를 실행하고 생성된 XML 문서를 화면에 표시합니다.  
  
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
         MemoryStream ms = new MemoryStream();  
         StreamWriter sw = new StreamWriter(ms);  
         ms.Position = 0;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandStream = new FileStream("TemplateFile.xml", FileMode.Open, FileAccess.Read);  
         cmd.CommandType = SqlXmlCommandType.Template;  
         using (Stream strm = cmd.ExecuteStream())  
         {  
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
  
1.  이 예에서 제공하는 XML 템플릿(TemplateFile.xml)을 폴더에 저장합니다.  
  
2.  이 예에서 제공하는 C# 코드(DocSample.cs)를 스키마가 저장된 폴더와 같은 폴더에 저장합니다. (다른 폴더에 파일을 저장하는 경우 코드를 편집하여 매핑 스키마에 대해 적합한 디렉터리 경로를 지정해야 합니다.)  
  
3.  코드를 컴파일합니다. 다음을 사용하여 명령 프롬프트에서 코드를 컴파일합니다.  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     이렇게 하면 실행 파일(DocSample.exe)이 만들어집니다.  
  
4.  명령 프롬프트에서 DocSample.exe를 실행합니다.  
  
  
