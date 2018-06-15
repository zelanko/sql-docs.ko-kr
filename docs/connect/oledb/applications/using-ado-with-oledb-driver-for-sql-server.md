---
title: OLE DB 드라이버와 함께 ADO를 사용 하 여 SQL server | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버와 함께 ADO를 사용
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 89f11eda93f9ac8eb67259265b646a2544143ae5
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612198"
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>SQL Server 용 OLE DB 드라이버와 함께 ADO를 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  에 도입 된 새로운 기능을 활용 하기 위해 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 여러 활성 결과 집합 (MARS), 쿼리 알림, 사용자 정의 형식 (Udt) 또는 새 같은 **xml** 데이터 형식으로 ActiveX을 사용 하는 기존 응용 프로그램 데이터 개체 (ADO)으로 데이터 액세스 공급자의 SQL Server 용 OLE DB 드라이버를 사용 해야 합니다.  
  
 최신 버전의 새로운 기능을 사용 하도록 ADO를 사용 하도록 설정 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 몇 가지 향상 된 기능에 적용 된 OLE DB Driver OLE DB의 핵심 기능을 확장 하는 SQL Server에 대 한 합니다. 이러한 개선 사항을 통해 사용 하도록 ADO 응용 프로그램을 최신 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능 및에 도입 된 형식에서는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** 및 **udt**합니다. 이러한 향상 된이 기능에 대 한 향상도 악용 하는 **varchar**, **nvarchar**, 및 **varbinary** 데이터 형식입니다. OLE DB Driver for SQL Server는 DBPROPSET_SQLSERVERDBINIT 속성 집합에 사용 하 여 ADO 응용 프로그램에서 새 데이터 형식이 ADO와 맞는 방식으로 노출 됩니다에 SSPROP_INIT_DATATYPECOMPATIBILITY 초기화 속성을 추가 합니다. 또한는 OLE DB Driver for SQL Server 라는 새로운 연결 문자열 키워드를도 정의 **DataTypeCompatibility** 연결 문자열에 설정 된 합니다.  

> [!NOTE]  
>  기존 ADO 응용 프로그램은 SQLOLEDB 공급자를 사용하여 XML, UDT, 큰 값 텍스트 및 이진 필드 값을 액세스하고 업데이트할 수 있습니다. 새 큰 **varchar (max)**, **nvarchar (max)**, 및 **varbinary (max)** 데이터 형식은 ADO 형식으로 반환 됩니다 **adLongVarChar**, **adLongVarWChar** 및 **adLongVarBinary** 각각. XML 열으로 반환 됩니다 **adLongVarChar**, UDT 열으로 반환 되 고 **adVarBinary**합니다. 그러나 경우에 대 한 SQL Server (MSOLEDBSQL) SQLOLEDB 대신 OLE DB 드라이버를 사용 해야 설정 하는 **DataTypeCompatibility** 키워드를 "80" ADO 데이터 형식에 새 데이터 형식이 올바르게 매핑되는지 되도록 합니다.  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>ADO에서 SQL Server 용 OLE DB 드라이버를 사용 하도록 설정  
 SQL Server 용 OLE DB 드라이버의 사용을 사용 하려면 ADO 응용 프로그램은 연결 문자열에 다음 키워드를 구현 해야 합니다.  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 ADO에 대 한 자세한 정보에 대 한 연결 문자열 SQL Server 용 OLE DB 드라이버에서 지원 되는 키워드 참조 [OLE DB 드라이버와 SQL Server에 대 한 연결 문자열 키워드를 사용 하 여](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)합니다.  

 다음은 MARS 기능 사용을 포함 한 SQL Server 용 OLE DB 드라이버와 함께 사용 하 여 완벽 하 게 설정 된 ADO 연결 문자열을 설정 하는 예입니다.  

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
 다음 섹션에서는 SQL Server에 대 한 OLE DB 드라이버와 함께 ADO를 사용 하는 방법의 예제를 제공 합니다.  

### <a name="retrieving-xml-column-data"></a>XML 열 데이터 검색  
 이 예제에서는 레코드 집합 검색 및의 XML 열에서 데이터를 표시 하는 데 사용 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** 예제 데이터베이스.  

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
 이 예제는 **명령** 개체를 사용 하 여 UDT를 반환 하는 SQL 쿼리를 실행할 수, UDT 데이터 업데이트 되 고 데이터베이스에 다시 새 데이터를 삽입 하는 다음 합니다. 이 예에서는 가정 하 고 **지점** UDT는 데이터베이스에 이미 등록 되었습니다.  

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
 이 예제에서는 연결 문자열이 SQL Server 용 OLE DB 드라이버를 통해 MARS를 사용 하도록 구성 됩니다 및 다음 두 개의 레코드 집합 개체가 만들어져 같은 연결을 사용 하 여 실행 합니다.  

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

 이전 버전의 OLE DB 공급자에서는 단일 연결당 하나의 활성 결과 집합만 열 수 있었으므로 이 코드를 두 번째로 실행하면 암시적 연결이 만들어집니다. 암시적 연결은 OLE DB 연결 풀에서 풀링되지 않았으므로 이로 인해 추가 오버헤드가 발생했습니다. SQL Server 용 OLE DB 드라이버에 의해 표시 MARS 기능을 사용 하면 하나의 연결에서 여러 활성 결과를 가져옵니다.  

## <a name="see-also"></a>관련 항목  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
