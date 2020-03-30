---
title: XML 값을 매개 변수로 지정
description: 하나의 명령에 XML 데이터를 매개 변수로서 전달하는 방법을 보여줍니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 2c4d08b8-fc29-4614-97fa-29c8ff7ca5b3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: b4d0f31c8f5fbb282c880abaee62f05dc190bbfc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896656"
---
# <a name="specifying-xml-values-as-parameters"></a>XML 값을 매개 변수로 지정

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

쿼리에 값이 XML 문자열인 매개 변수가 필요한 경우 개발자는 **SqlXml** 데이터 형식의 인스턴스를 사용하여 이 값을 제공할 수 있습니다. 여기에 까다로운 기법이 적용되는 것은 아니며 SQL Server의 XML 열은 다른 데이터 형식과 똑같은 방법으로 매개 변수 값을 받아들입니다.  
  
## <a name="example"></a>예제  
다음 콘솔 애플리케이션에서는 **AdventureWorks** 데이터베이스에 새 테이블을 만듭니다. 이 새 테이블에는 **SalesID**라는 열과 **SalesInfo**라는 XML 열이 포함되어 있습니다.  
  
> [!NOTE]
>  **AdventureWorks** 샘플 데이터베이스는 SQL Server를 설치할 때 기본적으로 설치되지 않으며 SQL Server Setup을 실행하여 설치할 수 있습니다.  
  
이 예제에서는 새 테이블에 행을 삽입할 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체를 준비합니다. 저장된 파일에서는 **SalesInfo** 열에 필요한 XML 데이터를 제공합니다.  
  
예제를 실행하는 데 필요한 파일을 만들려면 프로젝트와 동일한 폴더에 새 텍스트 파일을 만듭니다. 파일 이름을 MyTestStoreData.xml로 지정합니다. 파일을 메모장에서 열고 다음 텍스트를 복사해 붙여넣습니다.  
  
```xml  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>International Bank</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1970</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>7000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>T1</Internet>  
  <NumberEmployees>2</NumberEmployees>  
</StoreSurvey>  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
using System.Xml;  
using System.Data.SqlTypes;  
  
class Class1  
{  
    static void Main()  
    {  
        using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
       {  
        connection.Open();  
        //  Create a sample table (dropping first if it already  
        //  exists.)  
  
        string commandNewTable =   
            "IF EXISTS (SELECT * FROM dbo.sysobjects " +   
            "WHERE id = " +  
                  "object_id(N'[dbo].[XmlDataTypeSample]') " +   
            "AND OBJECTPROPERTY(id, N'IsUserTable') = 1) " +   
            "DROP TABLE [dbo].[XmlDataTypeSample];" +   
            "CREATE TABLE [dbo].[XmlDataTypeSample](" +   
            "[SalesID] [int] IDENTITY(1,1) NOT NULL, " +   
            "[SalesInfo] [xml])";  
        SqlCommand commandAdd =   
                   new SqlCommand(commandNewTable, connection);  
        commandAdd.ExecuteNonQuery();  
        string commandText =   
            "INSERT INTO [dbo].[XmlDataTypeSample] " +   
            "([SalesInfo] ) " +   
            "VALUES(@xmlParameter )";  
        SqlCommand command =   
                  new SqlCommand(commandText, connection);  
  
        //  Read the saved XML document as a   
        //  SqlXml-data typed variable.  
        SqlXml newXml =   
            new SqlXml(new XmlTextReader("MyTestStoreData.xml"));  
  
        //  Supply the SqlXml value for the value of the parameter.  
        command.Parameters.AddWithValue("@xmlParameter", newXml);  
  
        int result = command.ExecuteNonQuery();  
        Console.WriteLine(result + " row was added.");  
        Console.WriteLine("Press Enter to continue.");  
        Console.ReadLine();  
    }  
  }  
  
    private static string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,              
        // you can retrieve it from a configuration file.   
        return "Data Source=(local);Integrated Security=true;" +  
        "Initial Catalog=AdventureWorks; ";  
    }  
}  
```  
  
## <a name="next-steps"></a>다음 단계
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server의 XML 데이터](xml-data-sql-server.md)
