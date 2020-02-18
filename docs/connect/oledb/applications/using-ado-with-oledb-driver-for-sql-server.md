---
title: SQL Server용 OLE DB 드라이버에서 ADO 사용 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에서 ADO 사용
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b7e8ab700404aee32140bc935443e5911e4a56db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67989243"
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에서 ADO 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  MARS(Multiple Active Result Sets), 쿼리 알림, UDT(사용자 정의 형식) 또는 새 **xml** 데이터 형식과 같은 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 새 기능을 사용하려면 ADO(ActiveX Data Objects)를 사용하는 기존 애플리케이션은 SQL Server용 OLE DB 드라이버를 데이터 액세스 공급자로 사용해야 합니다.  
  
 ADO에서 최신 버전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 새 기능을 사용할 수 있도록 OLE DB의 주요 기능이 확장된 것을 비롯해 SQL Server용 OLE DB 드라이버의 기능이 향상되었습니다. 이러한 기능 향상을 통해 ADO 애플리케이션에서는 최신 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능과 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 **xml** 및 **udt**의 두 데이터 형식을 사용할 수 있습니다. 또한 개선된 **varchar**, **nvarchar** 및 **varbinary** 데이터 형식도 활용할 수 있습니다. SQL Server용 OLE DB 드라이버에서는 SSPROP_INIT_DATATYPECOMPATIBILITY 초기화 속성을 DBPROPSET_SQLSERVERDBINIT 속성 집합에 추가하고 ADO 애플리케이션에서 사용하여 새 데이터 형식이 ADO와 맞는 방식으로 노출되도록 할 수 있습니다. 또한 OLE DB Driver for SQL Server에서는 연결 문자열에서 설정하는 **DataTypeCompatibility**라는 새로운 연결 문자열 키워드도 정의합니다.  

> [!NOTE]  
>  기존 ADO 애플리케이션은 SQLOLEDB 공급자를 사용하여 XML, UDT, 큰 값 텍스트 및 이진 필드 값을 액세스하고 업데이트할 수 있습니다. 더 큰 새 **varchar(max)** , **nvarchar(max)** 및 **varbinary(max)** 데이터 형식은 각각 ADO 형식 **adLongVarChar**, **adLongVarWChar** 및 **adLongVarBinary**로 변환됩니다. XML 열은 **adLongVarChar**로 반환되고 UDT 열은 **adVarBinary**로 반환됩니다. 그러나 SQLOLEDB 대신 OLE DB Driver for SQL Server(MSOLEDBSQL)를 사용하는 경우 새 데이터 형식이 ADO 데이터 형식에 올바르게 매핑되도록 **DataTypeCompatibility**라는 키워드를 "80"으로 설정해야 합니다.  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>ADO에서 OLE DB Driver for SQL Server 사용  
 SQL Server용 OLE DB 드라이버를 사용하려면 ADO 애플리케이션에서 연결 문자열에 다음 키워드를 구현해야 합니다.  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 SQL Server용 OLE DB Driver에서 지원되는 ADO 연결 문자열 키워드에 대한 내용은 [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)을 참조하세요.  

 다음은 MARS 기능을 비롯하여 SQL Server용 OLE DB 드라이버가 완전히 사용되도록 설정하는 ADO 연결 문자열의 설정 예입니다.  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  

## <a name="examples"></a>예  
 다음 섹션에서는 OLE DB Driver for SQL Server와 함께 ADO를 사용하는 방법의 예를 보여 줍니다.  

### <a name="retrieving-xml-column-data"></a>XML 열 데이터 검색  
 이 예에서는 레코드 집합을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** 샘플 데이터베이스의 XML 열에서 데이터를 검색하고 표시합니다.  

```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _   
         & "DataTypeCompatibility=80;"  

con.Open  

' Get the xml data as a recordset.  
Set rst.ActiveConnection = con  
rst.Source = "SELECT AdditionalContactInfo FROM Person.Contact " _  
   & "WHERE AdditionalContactInfo IS NOT NULL"  
rst.Open  

' Display the data in the recordset.  
While (Not rst.EOF)  
   sXMLResult = rst.Fields("AdditionalContactInfo").Value  
   Debug.Print (sXMLResult)  
   rst.MoveNext  
End While  

con.Close  
Set con = Nothing  
```  

> [!NOTE]  
>  XML 열에서는 레코드 집합 필터링은 지원하지 않으므로 사용하는 경우 오류가 반환됩니다.  

### <a name="retrieving-udt-column-data"></a>UDT 열 데이터 검색  
 이 예에서는 **Command** 개체를 사용하여 UDT를 반환하는 SQL 쿼리를 실행하고 UDT 데이터를 업데이트한 다음, 새 데이터를 데이터베이스에 다시 삽입합니다. 이 예에서는 **Point** UDT가 데이터베이스에 이미 등록되어 있다고 가정합니다.  

```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;"  

con.Open  

' Get the UDT value.  
Set cmd.ActiveConnection = con  
cmd.CommandText = "SELECT ID, Pnt FROM dbo.Points.ToString()"  
Set rst = cmd.Execute  
strTempID = rst.Fields(0).Value  
strOldUDT = rst.Fields(1).Value  

' Do something with the UDT by adding i to each point.  
arytempUDT = Split(strOldUDT, ",")  
i = 3  
strNewUDT = LTrim(Str(Int(aryTempUDT(0)) + i)) + "," + _  
   LTrim(Str(Int(aryTempUDT(1)) + i))  

' Insert the new value back into the database.  
cmd.CommandText = "UPDATE dbo.Points SET Pnt = '" + strNewUDT + _  
   "' WHERE ID = '" + strTempID + "'"  
cmd.Execute  

con.Close  
Set con = Nothing  
```  

### <a name="enabling-and-using-mars"></a>MARS 설정 및 사용  
 이 예에서는 연결 문자열을 생성하여 SQL Server용 OLE DB 드라이버를 통해 MARS를 사용하도록 설정한 다음, 같은 연결을 사용하여 실행할 두 개의 레코드 집합 개체를 만듭니다.  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  

Dim recordset1 As New ADODB.Recordset  
Dim recordset2 As New ADODB.Recordset  

Dim recordsaffected As Integer  
Set recordset1 =  con.Execute("SELECT * FROM Table1", recordsaffected, adCmdText)  
Set recordset2 =  con.Execute("SELECT * FROM Table2", recordsaffected, adCmdText)  

con.Close  
Set con = Nothing  
```  

 이전 버전의 OLE DB 공급자에서는 단일 연결당 하나의 활성 결과 집합만 열 수 있었으므로 이 코드를 두 번째로 실행하면 암시적 연결이 만들어집니다. 암시적 연결은 OLE DB 연결 풀에서 풀링되지 않았으므로 이로 인해 추가 오버헤드가 발생했습니다. SQL Server용 OLE DB 드라이버에서 MARS 기능을 노출하면 하나의 연결에서 여러 활성 결과를 열 수 있습니다.  

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
