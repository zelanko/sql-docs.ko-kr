---
title: UDT 데이터 검색 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SqlDataReader object
- ADO.NET [CLR integration]
- binding UDTs [CLR integration]
- UDTs [CLR integration], ADO.NET
- assemblies [CLR integration], user-defined types
- query parameters [CLR integration]
- user-defined types [CLR integration], ADO.NET
- bytes [CLR integration]
ms.assetid: 6a98ac8c-0e69-4c03-83a4-2062cb782049
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 085b1783214e7f629f1cb91084303edacd151c25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874639"
---
# <a name="retrieving-udt-data"></a>UDT 데이터 검색
  클라이언트에서 UDT(사용자 정의 형식)를 만들려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 UDT로 등록된 어셈블리를 클라이언트 응용 프로그램에서 사용할 수 있어야 합니다. UDT 어셈블리는 응용 프로그램과 같은 디렉터리나 GAC(전역 어셈블리 캐시)에 넣을 수 있습니다. 사용자의 프로젝트에서 어셈블리에 대한 참조를 설정할 수도 있습니다.  
  
## <a name="requirements-for-using-udts-in-adonet"></a>ADO.NET에서 UDT 사용을 위한 요구 사항  
 클라이언트에서 UDT를 만들려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드된 어셈블리와 클라이언트의 어셈블리가 호환되어야 합니다. `Native` 직렬화 형식으로 정의된 UDT의 경우 어셈블리가 구조적으로 호환되어야 하며, `UserDefined` 형식으로 정의된 어셈블리의 경우 클라이언트에서 어셈블리를 사용할 수 있어야 합니다.  
  
 클라이언트에 UDT 어셈블리의 복사본이 없어도 테이블의 UDT 열에서 원시 데이터를 검색할 수 있습니다.  
  
> [!NOTE]  
>  **SqlClient** UDT 버전이 일치 하지 또는 다른 문제가 발생할 경우 UDT를 로드 하지 못할 수 있습니다. 이 경우에는 일반적인 문제 해결 메커니즘을 사용하여 호출 응용 프로그램에서 UDT를 포함하는 어셈블리를 찾지 못하는 이유를 확인하십시오. 자세한 내용은 .NET Framework 설명서에서 제목이 "관리 디버깅 도우미를 사용하여 오류 진단"인 항목을 참조하십시오.  
  
## <a name="accessing-udts-with-a-sqldatareader"></a>SqlDataReader를 사용하여 UDT 액세스  
 클라이언트 코드에서 `System.Data.SqlClient.SqlDataReader`를 사용하여 UDT 열을 포함하는 결과 집합을 검색할 수 있습니다. 이러한 결과 집합은 개체의 인스턴스로 표시됩니다.  
  
### <a name="example"></a>예제  
 이 예에서는 `Main` 메서드를 사용하여 새로운 `SqlDataReader` 개체를 만드는 방법을 보여 줍니다. 코드 예제 내에서는 다음 동작이 수행됩니다.  
  
1.  Main 메서드가 새 `SqlDataReader` 개체를 만들고 Point라는 UDT 열이 있는 Points 테이블에서 값을 검색합니다.  
  
2.  Point UDT는 정수로 정의된 X 및 Y 좌표를 공개합니다.  
  
3.  UDT는 `Distance` 메서드와 `GetDistanceFromXY` 메서드를 정의합니다.  
  
4.  예제 코드에서 UDT의 기능을 설명하기 위해 기본 키 및 UDT 열의 값을 검색합니다.  
  
5.  예제 코드에서 `Point.Distance` 및 `Point.GetDistanceFromXY` 메서드를 호출합니다.  
  
6.  콘솔 창에 결과가 표시됩니다.  
  
> [!NOTE]  
>  응용 프로그램에 이미 UDT 어셈블리에 대한 참조가 있어야 합니다.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module ReadPoints  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the value of the UDT  
                Dim pnt As Point = CType(rdr(1), Point)  
  
             ' You can also use GetSqlValue and GetValue  
             ' Dim pnt As Point = CType(rdr.GetSqlValue(1), Point)  
             ' Dim pnt As Point = CType(rdr.GetValue(1), Point)  
  
                ' Print values  
                Console.WriteLine( _  
                 "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}", _  
                  id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance())  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
         & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
namespace Microsoft.Samples.SqlServer  
{  
class ReadPoints  
{  
static void Main()  
{  
  string connectionString = GetConnectionString();  
  using (SqlConnection cnn = new SqlConnection(connectionString))  
  {  
    cnn.Open();  
    SqlCommand cmd = new SqlCommand(  
       "SELECT ID, Pnt FROM dbo.Points", cnn);  
    SqlDataReader rdr = cmd.ExecuteReader();  
  
    while (rdr.Read())  
    {  
      // Retrieve the value of the Primary Key column  
      int id = rdr.GetInt32(0);  
  
        // Retrieve the value of the UDT  
        Point pnt = (Point)rdr[1];  
  
        // You can also use GetSqlValue and GetValue  
        // Point pnt = (Point)rdr.GetSqlValue(1);  
        // Point pnt = (Point)rdr.GetValue(1);  
  
        Console.WriteLine(  
        "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}",   
        id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance());  
    }  
  rdr.Close();  
  Console.WriteLine("done");  
  }  
  static private string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,   
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Initial Catalog=AdventureWorks;"  
        + "Integrated Security=SSPI";  
  }  
}  
```  
  
## <a name="binding-udts-as-bytes"></a>UDT를 바이트로 바인딩  
 UDT 열에서 원시 데이터를 검색하려는 경우가 있습니다. 로컬에서 데이터의 형식을 사용할 수 없거나 UDT의 인스턴스를 인스턴스화하지 않으려는 경우가 그러한 예입니다. 사용 하 여 바이트 배열에 원시 바이트를 읽을 수는 **GetBytes** 메서드를 `SqlDataReader`입니다. 이 메서드는 지정한 열 오프셋의 바이트 스트림을 지정한 버퍼 오프셋에서 시작하는 배열의 버퍼로 읽어 들입니다. 또 다른 옵션 중 하나를 사용 하는 것을 **GetSqlBytes** 또는 **GetSqlBinary** 메서드 모든 단일 작업에서 콘텐츠를 읽습니다. 어느 경우에나 UDT 개체는 인스턴스화되지 않으므로 클라이언트 어셈블리에서 UDT에 대한 참조를 설정하지 않아도 됩니다.  
  
### <a name="example"></a>예제  
 검색 하는 방법을 보여 주는이 예제는 **지점** 데이터를 사용 하 여 바이트 배열에 원시 바이트로 `SqlDataReader`합니다. 이 코드는 `System.Text.StringBuilder`를 사용하여 원시 바이트를 콘솔 창에 표시될 문자열 표현으로 변환합니다.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the raw bytes into a byte array  
                Dim buffer(31) As Byte  
                Dim byteCount As Integer = _  
                 CInt(rdr.GetBytes(1, 0, buffer, 0, 31))  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", buffer(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
        string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand("SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Retrieve the raw bytes into a byte array  
                byte[] buffer = new byte[32];  
                long byteCount = rdr.GetBytes(1, 0, buffer, 0, 32);  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", buffer[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
### <a name="example-using-getsqlbytes"></a>GetSqlBytes를 사용하는 예  
 검색 하는 방법을 보여 주는이 예제는 **지점** 데이터를 사용 하 여 단일 작업에서 원시 바이트로 합니다 **GetSqlBytes** 메서드. 이 코드는 `StringBuilder`를 사용하여 원시 바이트를 콘솔 창에 표시될 문자열 표현으로 변환합니다.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Use SqlBytes to retrieve raw bytes  
                Dim sb As SqlBytes = rdr.GetSqlBytes(1)  
                Dim byteCount As Long = sb.Length  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", sb(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
         string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Use SqlBytes to retrieve raw bytes  
                SqlBytes sb = rdr.GetSqlBytes(1);  
                long byteCount = sb.Length;  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", sb[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="working-with-udt-parameters"></a>UDT 매개 변수 작업  
 사용자의 ADO.NET 코드에서 UDT를 입력 및 출력 매개 변수 모두로 사용할 수 있습니다.  
  
## <a name="using-udts-in-query-parameters"></a>쿼리 매개 변수에 UDT 사용  
 `SqlParameter` 개체의 `System.Data.SqlClient.SqlCommand`를 설정할 때 UDT를 매개 변수 값으로 사용할 수 있습니다. `SqlDbType.Udt` 컬렉션에 대해 `SqlParameter` 메서드를 호출할 때는 매개 변수가 UDT임을 나타내기 위해 `Add` 개체의 `Parameters` 열거형을 사용합니다. `UdtTypeName` 의 속성을 `SqlCommand` 개체를 사용 하 여 데이터베이스에 UDT의 정규화 된 이름을 지정 하는 *database.schema_name.object_name* 구문입니다. 꼭 필요한 것은 아니지만 정규화된 이름을 사용하면 코드가 명확해집니다.  
  
> [!NOTE]  
>  클라이언트 프로젝트에서 UDT 어셈블리의 로컬 복사본을 사용할 수 있어야 합니다.  
  
### <a name="example"></a>예제  
 이 예의 코드에서는 `SqlCommand` 및 `SqlParameter` 개체를 만들어 테이블의 UDT 열에 데이터를 삽입합니다. 또한 `SqlDbType.Udt` 열거형을 사용하여 데이터 형식을 지정하며, `UdtTypeName` 개체에 `SqlParameter` 속성을 사용하여 데이터베이스에 UDT의 정규화된 이름을 지정합니다.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports system.Data  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim ConnectionString As String = GetConnectionString()  
    Dim cnn As New SqlConnection(ConnectionString)  
    Using cnn  
      Dim cmd As SqlCommand = cnn.CreateCommand()  
      cmd.CommandText = "INSERT INTO dbo.Points (Pnt) VALUES (@Point)"  
      cmd.CommandType = CommandType.Text  
  
      Dim param As New SqlParameter("@Point", SqlDbType.Udt)      param.UdtTypeName = "TestPoint.dbo.Point"      param.Direction = ParameterDirection.Input      param.Value = New Point(5, 6)      cmd.Parameters.Add(param)  
  
      cnn.Open()  
      cmd.ExecuteNonQuery()  
      Console.WriteLine("done")  
    End Using  
  End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  string ConnectionString = GetConnectionString();  
     using (SqlConnection cnn = new SqlConnection(ConnectionString))  
     {  
       SqlCommand cmd = cnn.CreateCommand();  
       cmd.CommandText =   
         "INSERT INTO dbo.Points (Pnt) VALUES (@Point)";  
       cmd.CommandType = CommandType.Text;  
  
       SqlParameter param = new SqlParameter("@Point", SqlDbType.Udt);       param.UdtTypeName = "TestPoint.dbo.Point";       param.Direction = ParameterDirection.Input;       param.Value = new Point(5, 6);       cmd.Parameters.Add(param);  
  
       cnn.Open();  
       cmd.ExecuteNonQuery();  
       Console.WriteLine("done");  
     }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [ADO.NET의 사용자 정의 형식 액세스](accessing-user-defined-types-in-ado-net.md)  
  
  
