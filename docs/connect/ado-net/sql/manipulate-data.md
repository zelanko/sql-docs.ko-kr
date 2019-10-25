---
title: 데이터 조작
description: MARS 응용 프로그램 코딩 예제를 제공 합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 51096a2e-8b38-4c4d-a523-799bfdb7ec69
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: df430bbacb69e1d95d001e4f9340ca60473503cd
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452166"
---
# <a name="manipulating-data"></a>데이터 조작

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

MARS (Multiple Active Result Sets)가 도입 되기 전에는 개발자가 여러 연결 또는 서버 쪽 커서를 사용 하 여 특정 시나리오를 해결 해야 했습니다. 또한 트랜잭션 상황에서 다중 연결을 사용하는 경우 **sp_getbindtoken** 및 **sp_bindsession**으로 바인딩된 연결을 사용해야 했습니다. 다음 시나리오에서는 여러 연결 대신 MARS 사용 연결을 사용 하는 방법을 보여 줍니다.  
  
## <a name="using-multiple-commands-with-mars"></a>MARS에서 여러 명령 사용  
다음 콘솔 응용 프로그램에서는 두 개의 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체와 MARS가 설정 된 단일 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체를 사용 하 여 두 개의 <xref:Microsoft.Data.SqlClient.SqlDataReader> 개체를 사용 하는 방법을 보여 줍니다.  
  
### <a name="example"></a>예제  
이 예에서는 **AdventureWorks** 데이터베이스에 대 한 단일 연결을 엽니다. @No__t_0 개체를 사용 하 여 <xref:Microsoft.Data.SqlClient.SqlDataReader>를 만듭니다. 판독기를 사용 하면 첫 번째 <xref:Microsoft.Data.SqlClient.SqlDataReader>의 데이터를 두 번째 판독기의 WHERE 절에 대 한 입력으로 사용 하 여 두 번째 <xref:Microsoft.Data.SqlClient.SqlDataReader> 열립니다.  
  
> [!NOTE]
>  다음 예제에서는 SQL Server에 포함된 샘플 **AdventureWorks** 데이터베이스를 사용합니다. 샘플 코드에 제공 된 연결 문자열은 데이터베이스가 로컬 컴퓨터에 설치 되어 있고 사용 가능한 지를 전제로 합니다. 사용자 환경에 필요한 경우 연결 문자열을 수정 합니다.  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  int vendorID;  
  SqlDataReader productReader = null;  
  string vendorSQL =   
    "SELECT VendorId, Name FROM Purchasing.Vendor";  
  string productSQL =   
    "SELECT Production.Product.Name FROM Production.Product " +  
    "INNER JOIN Purchasing.ProductVendor " +  
    "ON Production.Product.ProductID = " +   
    "Purchasing.ProductVendor.ProductID " +  
    "WHERE Purchasing.ProductVendor.VendorID = @VendorId";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    SqlCommand vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    SqlCommand productCmd =   
      new SqlCommand(productSQL, awConnection);  
  
    productCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    awConnection.Open();  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int)vendorReader["VendorId"];  
  
        productCmd.Parameters["@VendorId"].Value = vendorID;  
        // The following line of code requires  
        // a MARS-enabled connection.  
        productReader = productCmd.ExecuteReader();  
        using (productReader)  
        {  
          while (productReader.Read())  
          {  
            Console.WriteLine("  " +  
              productReader["Name"].ToString());  
          }  
        }  
      }  
  }  
      Console.WriteLine("Press any key to continue");  
      Console.ReadLine();  
    }  
  }  
  private static string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,  
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Integrated Security=SSPI;" +   
      "Initial Catalog=AdventureWorks;MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="reading-and-updating-data-with-mars"></a>MARS를 사용 하 여 데이터 읽기 및 업데이트  
MARS를 사용 하면 둘 이상의 보류 중인 작업을 포함 하는 읽기 작업 및 DML (데이터 조작 언어) 작업 모두에 대 한 연결을 사용할 수 있습니다. 이 기능을 사용 하면 응용 프로그램에서 연결 사용 오류를 처리할 필요가 없습니다. 또한 MARS는 일반적으로 더 많은 리소스를 사용 하는 서버 쪽 커서의 사용자를 대체할 수 있습니다. 마지막으로 여러 작업이 단일 연결에서 실행될 수 있으므로 동일한 트랜잭션 컨텍스트를 공유하여 **sp_getbindtoken** 및 **sp_bindsession** 시스템 저장 프로시저를 사용할 필요가 없습니다.  
  
### <a name="example"></a>예제  
다음 콘솔 응용 프로그램에서는 세 개의 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체와 MARS가 설정 된 단일 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체가 있는 두 개의 <xref:Microsoft.Data.SqlClient.SqlDataReader> 개체를 사용 하는 방법을 보여 줍니다. 첫 번째 명령 개체는 신용 등급이 5 인 공급 업체 목록을 검색 합니다. 두 번째 명령 개체는 <xref:Microsoft.Data.SqlClient.SqlDataReader>에서 제공한 공급 업체 ID를 사용 하 여 특정 공급 업체에 대 한 모든 제품과 함께 두 번째 <xref:Microsoft.Data.SqlClient.SqlDataReader>을 로드 합니다. 두 번째 <xref:Microsoft.Data.SqlClient.SqlDataReader>는 각 제품 레코드를 방문 합니다. 또한 새로운 **OnOrderQty**를 확인하기 위한 계산을 수행합니다. 그런 다음 세 번째 명령 개체를 사용하여 **ProductVendor** 테이블을 새 값으로 업데이트합니다. 이 전체 프로세스는 단일 트랜잭션 내에서 발생 하며,이는 끝에 롤백됩니다.  
  
> [!NOTE]
>  다음 예제에서는 SQL Server에 포함된 샘플 **AdventureWorks** 데이터베이스를 사용합니다. 샘플 코드에 제공 된 연결 문자열은 데이터베이스가 로컬 컴퓨터에 설치 되어 있고 사용 가능한 지를 전제로 합니다. 사용자 환경에 필요한 경우 연결 문자열을 수정 합니다.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Program  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  SqlTransaction updateTx = null;  
  SqlCommand vendorCmd = null;  
  SqlCommand prodVendCmd = null;  
  SqlCommand updateCmd = null;  
  
  SqlDataReader prodVendReader = null;  
  
  int vendorID = 0;  
  int productID = 0;  
  int minOrderQty = 0;  
  int maxOrderQty = 0;  
  int onOrderQty = 0;  
  int recordsUpdated = 0;  
  int totalRecordsUpdated = 0;  
  
  string vendorSQL =  
      "SELECT VendorID, Name FROM Purchasing.Vendor " +   
      "WHERE CreditRating = 5";  
  string prodVendSQL =  
      "SELECT ProductID, MaxOrderQty, MinOrderQty, OnOrderQty " +  
      "FROM Purchasing.ProductVendor " +   
      "WHERE VendorID = @VendorID";  
  string updateSQL =  
      "UPDATE Purchasing.ProductVendor " +   
      "SET OnOrderQty = @OrderQty " +  
      "WHERE ProductID = @ProductID AND VendorID = @VendorID";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    awConnection.Open();  
    updateTx = awConnection.BeginTransaction();  
  
    vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    vendorCmd.Transaction = updateTx;  
  
    prodVendCmd = new SqlCommand(prodVendSQL, awConnection);  
    prodVendCmd.Transaction = updateTx;  
    prodVendCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    updateCmd = new SqlCommand(updateSQL, awConnection);  
    updateCmd.Transaction = updateTx;  
    updateCmd.Parameters.Add("@OrderQty", SqlDbType.Int);  
    updateCmd.Parameters.Add("@ProductID", SqlDbType.Int);  
    updateCmd.Parameters.Add("@VendorID", SqlDbType.Int);  
  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int) vendorReader["VendorID"];  
        prodVendCmd.Parameters["@VendorID"].Value = vendorID;  
        prodVendReader = prodVendCmd.ExecuteReader();  
  
        using (prodVendReader)  
        {  
          while (prodVendReader.Read())  
          {  
            productID = (int) prodVendReader["ProductID"];  
  
            if (prodVendReader["OnOrderQty"] == DBNull.Value)  
            {  
              minOrderQty = (int) prodVendReader["MinOrderQty"];  
              onOrderQty = minOrderQty;  
            }  
            else  
            {  
              maxOrderQty = (int) prodVendReader["MaxOrderQty"];  
              onOrderQty = (int)(maxOrderQty / 2);  
            }  
  
            updateCmd.Parameters["@OrderQty"].Value = onOrderQty;  
            updateCmd.Parameters["@ProductID"].Value = productID;  
            updateCmd.Parameters["@VendorID"].Value = vendorID;  
  
            recordsUpdated = updateCmd.ExecuteNonQuery();  
            totalRecordsUpdated += recordsUpdated;  
          }  
        }  
      }  
    }  
    Console.WriteLine("Total Records Updated: " +   
      totalRecordsUpdated.ToString());  
    updateTx.Rollback();  
    Console.WriteLine("Transaction Rolled Back");  
  }  
  
  Console.WriteLine("Press any key to continue");  
  Console.ReadLine();  
}  
private static string GetConnectionString()  
{  
  // To avoid storing the connection string in your code,  
  // you can retrieve it from a configuration file.  
  return "Data Source=(local);Integrated Security=SSPI;" +   
    "Initial Catalog=AdventureWorks;" +   
    "MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="next-steps"></a>다음 단계
- [MARS(Multiple Active Result Sets)](multiple-active-result-sets-mars.md)
