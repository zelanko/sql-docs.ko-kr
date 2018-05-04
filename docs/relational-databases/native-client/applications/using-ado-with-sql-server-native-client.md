---
title: SQL Server Native Client와 함께 ADO 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b09d3542cfd741771b70d29b55463482caf02503
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-ado-with-sql-server-native-client"></a>SQL Server Native Client와 함께 ADO 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  에 도입 된 새로운 기능을 활용 하기 위해 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 여러 활성 결과 집합 (MARS), 쿼리 알림, 사용자 정의 형식 (Udt) 또는 새 같은 **xml** 데이터 형식으로 ActiveX을 사용 하는 기존 응용 프로그램 데이터 개체 (ADO)를 사용 해야는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 데이터 액세스 공급자로 합니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 새 기능과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용할 필요가 없으면 현재 데이터 액세스 공급자 즉, 일반적으로 SQLOLEDB를 계속 사용할 수 있습니다. 기존 응용 프로그램을 개선하는 경우나 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 새 기능을 사용해야 하는 경우에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용해야 합니다.  
  
> [!NOTE]  
>  새 응용 프로그램을 개발하는 경우에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 대신 ADO.NET 및 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하여 최신 버전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 모든 새 기능에 액세스하는 것이 좋습니다. .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 자세한 내용은 ADO.NET에 대한 .NET Framework SDK 설명서를 참조하십시오.  
  
 ADO에서 최신 버전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 새 기능을 사용할 수 있도록 OLE DB의 주요 기능이 확장된 것을 비롯해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 기능이 향상되었습니다. 이러한 개선 사항을 통해 사용 하도록 ADO 응용 프로그램을 최신 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능 및에 도입 된 형식에서는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** 및 **udt**합니다. 이러한 향상 된이 기능에 대 한 향상도 악용 하는 **varchar**, **nvarchar**, 및 **varbinary** 데이터 형식입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 DBPROPSET_SQLSERVERDBINIT 속성 집합에 사용 하 여 ADO 응용 프로그램에서 새 데이터 형식이 ADO와 맞는 방식으로 노출 됩니다에 SSPROP_INIT_DATATYPECOMPATIBILITY 초기화 속성을 추가 합니다. 또한는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 또한 라는 새로운 연결 문자열 키워드 정의 **DataTypeCompatibility** 연결 문자열에 설정 된 합니다.  
  
> [!NOTE]  
>  기존 ADO 응용 프로그램은 SQLOLEDB 공급자를 사용하여 XML, UDT, 큰 값 텍스트 및 이진 필드 값을 액세스하고 업데이트할 수 있습니다. 새 큰 **varchar (max)**, **nvarchar (max)**, 및 **varbinary (max)** 데이터 형식은 ADO 형식으로 반환 됩니다 **adLongVarChar**, **adLongVarWChar** 및 **adLongVarBinary** 각각. XML 열으로 반환 됩니다 **adLongVarChar**, UDT 열으로 반환 되 고 **adVarBinary**합니다. 그러나 사용 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설정 되었는지 확인 해야 하는 SQLOLEDB 대신 Native Client OLE DB 공급자 (SQLNCLI11)는 **DataTypeCompatibility** 키워드를 "80" ADO 데이터에 새 데이터 형식이 올바르게 매핑되는지 있도록 형식입니다.  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>AOD에서 Server Native Client 사용  
 사용 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, ADO 응용 프로그램은 연결 문자열에는 다음 키워드를 구현 해야 합니다.  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 ADO에 대 한 자세한 정보에 대 한 연결 문자열에서 지원 되는 키워드 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native client를 [Connection String Keywords with SQL Server Native Client를 사용 하 여](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)합니다.  
  
 다음은이 완벽 하 게 작업할 수 있도록 설정 하는 ADO 연결 문자열을 설정 하는 예 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 MARS 기능 사용을 포함 한:  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  
  
## <a name="examples"></a>예  
 다음 섹션에서는 사용 하 여 ADO를 사용 하는 방법의 예는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다.  
  
### <a name="retrieving-xml-column-data"></a>XML 열 데이터 검색  
 이 예제에서는 레코드 집합 검색 및의 XML 열에서 데이터를 표시 하는 데 사용 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** 예제 데이터베이스.  
  
```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
 이 예제에서는 연결 문자열을 통해 MARS를 사용 하도록 생성 됩니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 다음의 두 레코드 집합 개체가 동일한 연결을 사용 하 여 실행에 생성 됩니다.  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
  
 이전 버전의 OLE DB 공급자에서는 단일 연결당 하나의 활성 결과 집합만 열 수 있었으므로 이 코드를 두 번째로 실행하면 암시적 연결이 만들어집니다. 암시적 연결은 OLE DB 연결 풀에서 풀링되지 않았으므로 이로 인해 추가 오버헤드가 발생했습니다. MARS 기능에 의해 노출 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 하면 하나의 연결에서 여러 활성 결과 얻을 Native Client OLE DB 공급자입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client 사용한 응용 프로그램 작성](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
