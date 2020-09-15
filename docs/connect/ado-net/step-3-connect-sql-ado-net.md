---
title: '3단계: ADO.NET을 사용하여 SQL에 연결하는 개념 증명 | Microsoft Docs'
description: SQL Server 연결, 쿼리 실행, 행 삽입을 수행하는 C# 코드 예시가 포함됩니다.
ms.custom: ''
ms.date: 08/05/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aebe3dc6-3ee4-4d11-8e43-5d32b3f91490
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 5e68e4e7753126c995923f0c037f227572a17e7f
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823378"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-adonet"></a>3단계: ADO.NET을 사용하여 SQL에 연결하는 개념 증명

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

- 이전 문서:&nbsp;&nbsp;&nbsp;[2단계: ADO.NET 개발을 위한 SQL 데이터베이스 만들기](step-2-create-sql-database-ado-net-development.md)  
- 다음 문서:&nbsp;&nbsp;&nbsp;[4단계: ADO.NET으로 SQL에 탄력적으로 연결](step-4-connect-resiliently-sql-ado-net.md)  

  
이 C# 코드 예제는 개념 증명으로만 간주되어야 합니다. 이 샘플 코드는 명확히 이해할 수 있도록 단순화되었으며 Microsoft에서 권장하는 모범 사례를 대표하는 것은 아닙니다.  
  
## <a name="step-1-connect"></a>1단계: 연결
  
**SqlConnection.Open** 메서드는 SQL 데이터베이스에 연결하는 데 사용됩니다.  


```csharp
using System;
using QC = Microsoft.Data.SqlClient;
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  

                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
Press any key to finish...  
****/  
```  


## <a name="step-2-execute-a-query"></a>2단계: 쿼리 실행  
  
SqlCommand.ExecuteReader 메서드는 다음과 같습니다.  
  
- SQL SELECT 문을 SQL 시스템으로 실행합니다.  
- SqlDataReader 인스턴스를 반환하여 결과 행에 대한 액세스를 제공합니다.  
  
  
  
```csharp
using System;
using DT = System.Data;
using QC = Microsoft.Data.SqlClient;
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.SelectRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void SelectRows(QC.SqlConnection connection)  
        {  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
SELECT  
    TOP 5  
        COUNT(soh.SalesOrderID) AS [OrderCount],  
        c.CustomerID,  
        c.CompanyName  
    FROM  
                        SalesLT.Customer         AS c  
        LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh  
            ON c.CustomerID = soh.CustomerID  
    GROUP BY  
        c.CustomerID,  
        c.CompanyName  
    ORDER BY  
        [OrderCount] DESC,  
        c.CompanyName; ";  
  
                QC.SqlDataReader reader = command.ExecuteReader();  
  
                while (reader.Read())  
                {  
                    Console.WriteLine("{0}\t{1}\t{2}",  
                        reader.GetInt32(0),  
                        reader.GetInt32(1),  
                        reader.GetString(2));  
                }  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
1       29736   Action Bicycle Specialists  
1       29638   Aerobic Exercise Company  
1       29546   Bulk Discount Store  
1       29741   Central Bicycle Specialists  
1       29612   Channel Outlet  
Press any key to finish...  
****/  
```  
  
  
  
## <a name="step-3-insert-a-row"></a>3단계: 행 삽입  
  
  
이 예에서는 다음을 수행하는 방법을 보여 줍니다.  
  
- 매개 변수를 전달하여 SQL INSERT 문을 실행합니다.  
  - 매개 변수를 사용하여 SQL 삽입 공격으로부터 보호합니다.  
- 자동 생성된 값을 검색합니다.  
  
  
  
```csharp
using System;
using DT = System.Data;
using QC = Microsoft.Data.SqlClient;
  
namespace ProofOfConcept_SQL_CSharp  
{  
    public class Program  
    {  
        static public void Main()  
        {  
            using (var connection = new QC.SqlConnection(  
                "Server=tcp:YOUR_SERVER_NAME_HERE.database.windows.net,1433;" +
                "Database=AdventureWorksLT;User ID=YOUR_LOGIN_NAME_HERE;" +
                "Password=YOUR_PASSWORD_HERE;Encrypt=True;" +
                "TrustServerCertificate=False;Connection Timeout=30;"  
                ))  
            {  
                connection.Open();  
                Console.WriteLine("Connected successfully.");  
  
                Program.InsertRows(connection);  
  
                Console.WriteLine("Press any key to finish...");  
                Console.ReadKey(true);  
            }  
        }  
  
        static public void InsertRows(QC.SqlConnection connection)  
        {  
            QC.SqlParameter parameter;  
  
            using (var command = new QC.SqlCommand())  
            {  
                command.Connection = connection;  
                command.CommandType = DT.CommandType.Text;  
                command.CommandText = @"  
INSERT INTO SalesLT.Product  
        (Name,  
        ProductNumber,  
        StandardCost,  
        ListPrice,  
        SellStartDate  
        )  
    OUTPUT  
        INSERTED.ProductID  
    VALUES  
        (@Name,  
        @ProductNumber,  
        @StandardCost,  
        @ListPrice,  
        CURRENT_TIMESTAMP  
        ); ";  
  
                parameter = new QC.SqlParameter("@Name", DT.SqlDbType.NVarChar, 50);  
                parameter.Value = "SQL Server Express 2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ProductNumber", DT.SqlDbType.NVarChar, 25);  
                parameter.Value = "SQLEXPRESS2014";  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@StandardCost", DT.SqlDbType.Int);  
                parameter.Value = 11;  
                command.Parameters.Add(parameter);  
  
                parameter = new QC.SqlParameter("@ListPrice", DT.SqlDbType.Int);  
                parameter.Value = 12;  
                command.Parameters.Add(parameter);  
  
                int productId = (int)command.ExecuteScalar();  
                Console.WriteLine("The generated ProductID = {0}.", productId);  
            }  
        }  
    }  
}  
/**** Actual output:  
Connected successfully.  
The generated ProductID = 1000.  
Press any key to finish...  
****/  
```
