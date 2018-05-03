---
title: '3 단계: ADO.NET을 사용 하 여 SQL에 연결 하는 개념 증명 | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado-net
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: aebe3dc6-3ee4-4d11-8e43-5d32b3f91490
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31c30cd37e9408528a415986da9ba4b73fb73aae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-adonet"></a>3 단계: ADO.NET을 사용 하 여 SQL에 연결 하는 개념 증명

- 이전 문서:&nbsp;&nbsp;&nbsp;[2 단계: ADO.NET 개발에 대 한 SQL 데이터베이스 만들기](step-2-create-a-sql-database-for-ado-net-development.md)  
- 다음 문서:&nbsp;&nbsp;&nbsp;[4 단계: 탄력적 ado.net SQL에 연결](step-4-connect-resiliently-to-sql-with-ado-net.md)  

  
이 C# 코드 예제에서는 개념 증명을 고려 되어야 합니다. 샘플 코드의 명확성을 위해 간소화 되 고 Microsoft에서 권장 모범 사례 나타내지는지 않습니다.  
  
## <a name="step-1-connect"></a>1 단계: 연결
  
메서드가 **SqlConnection.Open** SQL 데이터베이스에 연결 하는 데 사용 됩니다.  


```CSharp  
    // C# , ADO.NET  
    using System;
    using QC = System.Data.SqlClient;  // System.Data.dll  
      
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


## <a name="step-2--execute-a-query"></a>2 단계: 쿼리를 실행 합니다.  
  
SqlCommand.ExecuteReader 메서드:  
  
- SQL 시스템에 SQL SELECT 문을 실행합니다.  
- 결과 행에 대 한 액세스를 제공 하는 SqlDataReader의 인스턴스를 반환 합니다.  
  
  
  
```CSharp  
    using System;  // C# , ADO.NET  
    using DT = System.Data;            // System.Data.dll  
    using QC = System.Data.SqlClient;  // System.Data.dll  
      
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
  
  
  
## <a name="step-3-insert-a-row"></a>행을 삽입 하는 3 단계:  
  
  
이 예제에서는 하는 방법:  
  
- SQL INSERT 문을 매개 변수를 전달 하 여 안전 하 게 실행 합니다.  
  - SQL 삽입 공격 으로부터 보호 하는 매개 변수를 사용 합니다.  
- 자동 생성 된 값을 검색 합니다.  
  
  
  
```CSharp  
    using System;  // C# , ADO.NET  
    using DT = System.Data;            // System.Data.dll  
    using QC = System.Data.SqlClient;  // System.Data.dll  
      
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
