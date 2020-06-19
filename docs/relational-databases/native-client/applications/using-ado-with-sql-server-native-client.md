---
title: ADO 사용
description: SQL Server 2005에 도입 된 새 기능을 사용 하려면 ADO를 사용 하는 기존 응용 프로그램에서 SQL Server Native Client OLE DB 공급자를 사용 해야 합니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 47a7021093710c8ebb4e300880ea58af037dcd70
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84949596"
---
# <a name="using-ado-with-sql-server-native-client"></a>SQL Server Native Client와 함께 ADO 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]MARS (multiple active result sets), 쿼리 알림, udt (사용자 정의 형식) 또는 새로운 **xml** 데이터 형식과 같은에 도입 된 새 기능을 활용 하기 위해 ADO (ADO(ActiveX Data Objects))를 사용 하는 기존 응용 프로그램은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 데이터 액세스 공급자로 사용 해야 합니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 새 기능과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용할 필요가 없으면 현재 데이터 액세스 공급자 즉, 일반적으로 SQLOLEDB를 계속 사용할 수 있습니다. 기존 애플리케이션을 개선하는 경우나 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 새 기능을 사용해야 하는 경우에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용해야 합니다.  
  
> [!NOTE]  
>  새 애플리케이션을 개발하는 경우에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 대신 ADO.NET 및 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하여 최신 버전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 모든 새 기능에 액세스하는 것이 좋습니다. .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 자세한 내용은 ADO.NET에 대한 .NET Framework SDK 설명서를 참조하십시오.  
  
 ADO에서 최신 버전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 새 기능을 사용할 수 있도록 OLE DB의 주요 기능이 확장된 것을 비롯해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 기능이 향상되었습니다. 이러한 기능 향상을 통해 ADO 애플리케이션에서는 최신 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능과 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 **xml** 및 **udt**의 두 데이터 형식을 사용할 수 있습니다. 또한 개선된 **varchar**, **nvarchar** 및 **varbinary** 데이터 형식도 활용할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client는 ado 응용 프로그램에서 사용할 DBPROPSET_SQLSERVERDBINIT 속성 집합에 SSPROP_INIT_DATATYPECOMPATIBILITY 초기화 속성을 추가 하 여 ADO와 호환 되는 방식으로 새 데이터 형식을 노출 합니다. 또한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 연결 문자열에 설정 된 **DataTypeCompatibility** 이라는 새 연결 문자열 키워드를 정의 합니다.  
  
> [!NOTE]  
>  기존 ADO 애플리케이션은 SQLOLEDB 공급자를 사용하여 XML, UDT, 큰 값 텍스트 및 이진 필드 값을 액세스하고 업데이트할 수 있습니다. 더 큰 새 **varchar(max)** , **nvarchar(max)** 및 **varbinary(max)** 데이터 형식은 각각 ADO 형식 **adLongVarChar**, **adLongVarWChar** 및 **adLongVarBinary**로 변환됩니다. XML 열은 **adLongVarChar**로 반환되고 UDT 열은 **adVarBinary**로 반환됩니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLOLEDB 대신 Native CLIENT SQLNCLI11 (OLE DB provider)를 사용 하는 경우 새 데이터 형식이 ADO 데이터 형식에 올바르게 매핑되도록 **DataTypeCompatibility** 키워드를 "80"로 설정 해야 합니다.  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>AOD에서 Server Native Client 사용  
 Native Client를 사용 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ADO 응용 프로그램에서 연결 문자열에 다음 키워드를 구현 해야 합니다.  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 Native Client에서 지원 되는 ADO 연결 문자열 키워드에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQL Server Native Client 연결 문자열 키워드 사용](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조 하세요.  
  
 다음은 MARS 기능의 사용을 비롯 하 여 Native Client와 함께 작동 하도록 완전히 활성화 된 ADO 연결 문자열을 설정 하는 예입니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
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
 다음 섹션에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자와 함께 ADO를 사용 하는 방법에 대 한 예제를 제공 합니다.  
  
### <a name="retrieving-xml-column-data"></a>XML 열 데이터 검색  
 이 예에서는 레코드 집합을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** 샘플 데이터베이스의 XML 열에서 데이터를 검색하고 표시합니다.  
  
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
 이 예에서는 Native Client OLE DB 공급자를 통해 MARS를 사용 하도록 설정 하기 위해 연결 문자열이 생성 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다음 동일한 연결을 사용 하 여 실행 하기 위해 두 개의 레코드 집합 개체가 생성 됩니다.  
  
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
  
 이전 버전의 OLE DB 공급자에서는 단일 연결당 하나의 활성 결과 집합만 열 수 있었으므로 이 코드를 두 번째로 실행하면 암시적 연결이 만들어집니다. 암시적 연결은 OLE DB 연결 풀에서 풀링되지 않았으므로 이로 인해 추가 오버헤드가 발생했습니다. Native Client OLE DB 공급자가 제공 하는 MARS 기능 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 을 사용 하면 하나의 연결에서 여러 활성 결과를 얻을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client를 사용하여 애플리케이션 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
