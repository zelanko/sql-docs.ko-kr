---
title: ADO (SQLXML)를 사용 하 여 Updategram 실행
description: Microsoft SQL Server 인스턴스에 대 한 연결을 설정 하 고 ADO (SQLXML 4.0)를 사용 하 여 updategram.by를 실행 하는 방법에 대해 알아봅니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- ADO [SQLXML]
- updategrams [SQLXML], ADO
- executing updategrams [SQLXML]
ms.assetid: 78610ca0-f763-45fc-ac64-da5c192cc3e5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 325ef35c27f97f99902c927fce6e3eb268035ccf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462874"
---
# <a name="executing-an-updategram-by-using-ado-sqlxml-40"></a>ADO를 사용하여 updategram 실행(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  이 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 애플리케이션은 ADO를 사용하여 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하고 updategram을 실행합니다. 사용되는 updategram은 특정 직원의 성을 업데이트합니다. 이 예에서는 AdventureWorks 예제 데이터베이스를 사용합니다.  
  
 이 예제 애플리케이션에서는 다음 작업이 수행됩니다.  
  
-   **Conn** 개체 (**ADODB. 연결**) 특정 서버 컴퓨터에서 실행 중인 인스턴스에 대 한 연결을 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 합니다.  
  
-   **Cmd** 개체 (**ADODB 명령**)는 설정 된 연결에서 실행 됩니다.  
  
-   명령 언어가 DBGUID_MSSQLXML로 설정됩니다.  
  
-   Updategram가 명령 스트림 (**Strmin**)에 복사 됩니다.  
  
-   명령의 출력 스트림은 **Strmout** 개체 (**ADODB. Stream**)을 클릭 하 여 반환 된 데이터를 수신 합니다.  
  
-   최종적으로 명령(updategram)이 실행됩니다.  
  
 다음은 예제 코드입니다.  
  
```vb  
Private Sub Form_Load()  
  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmIn As New ADODB.Stream  
  Dim strmOut As New ADODB.Stream  
  Dim SQLxml As String  
  
  ' Open a connection to the instance of SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=(local); database=AdventureWorks; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  
  ' Build the command string in the form of an XML template.  
    SQLxml = "<ROOT xmlns:updg='urn:schemas-microsoft-com:xml-updategram' >"  
    SQLxml = SQLxml & "  <updg:sync updg:nullvalue='IsNULL'>"  
    SQLxml = SQLxml & "    <updg:before>"  
    SQLxml = SQLxml & "       <Person.Contact ContactID='64' Title='IsNULL'/>"  
    SQLxml = SQLxml & "    </updg:before>"  
    SQLxml = SQLxml & "    <updg:after>"  
    SQLxml = SQLxml & "       <Person.Contact ContactID='64' Title='Mr.'/>"  
    SQLxml = SQLxml & "    </updg:after>"  
    SQLxml = SQLxml & "  </updg:sync>"  
    SQLxml = SQLxml & "</ROOT>"  
  
  ' Set the command dialect to DBGUID_MSSQLXML.  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
  ' Open the command stream and write our template to it.  
  strmIn.Open  
  strmIn.WriteText SQLxml  
  strmIn.Position = 0  
  
  Set cmd.CommandStream = strmIn  
  
  ' Execute the command, open the return stream, and read the result.  
  strmOut.Open  
  strmOut.LineSeparator = adCRLF  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Debug.Print strmOut.ReadText  
  strmOut.Close  
  strmIn.Close  
  
End Sub  
  
```  
  
> [!NOTE]  
>  XSD 스키마를 지정하는 updategram을 실행하기 위해 ADO에서 SQLXML을 사용하는 경우 다음 코드 예에서 볼 수 있듯이 연결 개체의 "`SQLXML Version`" 속성을 "`SQLXML.4.0`"으로 설정해야 합니다.  
>   
>  `conn.Properties("SQLXML Version") = "SQLXML.4.0"`  
  
## <a name="specifying-a-mapping-schema-for-the-updategram"></a>updategram에 대한 매핑 스키마 지정  
 이 예에서는 updategram에 매핑 스키마를 지정하고 사용하는 방법을 보여 줍니다.  
  
 다음 XSD 스키마(EmpSchema.xml)를 디스크에 저장하고 이 코드에 지정된 경로를 디스크에서 매핑 스키마가 저장된 위치로 업데이트하십시오. 이 코드에서는 스키마가 C: 드라이브의 Schemas 폴더에 저장되어 있다고 가정합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
        <xsd:attribute name="CID"    
                       sql:field="ContactID"   
                       type="xsd:string" />   
        <xsd:attribute name="MName"    
                       sql:field="MiddleName"    
                       type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 XSD 및 XDR 스키마를 모두 지정할 수 있습니다. 다음은 동일한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
   <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
         xmlns:dt="urn:schemas-microsoft-com:datatypes"   
         xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
     <ElementType name="Contact" sql:relation="Person.Contact" >  
       <AttributeType name="CID" />  
       <AttributeType name="MName" />  
  
       <attribute type="CID" sql:field="ContactID" />  
       <attribute type="MName" sql:field="MiddleName" />  
     </ElementType>  
   </Schema>   
```  
  
 다음은 연결된 매핑 스키마가 있는 updategram을 실행하기 위한 Visual Basic 코드입니다. 이 updategram은 Person.Contact 테이블에 있는 연락처 1의 중간 이름을 업데이트합니다.  
  
```vb  
Private Sub Form_Load()  
    Dim cmd As New ADODB.Command  
    Dim conn As New ADODB.Connection  
    Dim strmIn As New ADODB.Stream  
    Dim strmOut As New ADODB.Stream  
  
    ' Open a connection to the SQL Server.  
    conn.Provider = "SQLOLEDB"  
    conn.Open "server=(local); database=AdventureWorks; Integrated Security='SSPI' ;"  
    conn.Properties("SQLXML Version") = "SQLXML.4.0"  
    Set cmd.ActiveConnection = conn  
  
    ' Open the command stream and write the template to it.  
    strmIn.Open  
    strmIn.WriteText "<ROOT xmlns:updg='urn:schemas-microsoft-com:xml-updategram' >"  
    strmIn.WriteText "  <updg:sync mapping-schema='C:\Schemas\EmpSchema.xml' >"  
    strmIn.WriteText "      <updg:before>"  
    strmIn.WriteText "          <Contact CID='1' />"  
    strmIn.WriteText "      </updg:before>"  
    strmIn.WriteText "      <updg:after>"  
    strmIn.WriteText "          <Contact MName='M.'/>"  
    strmIn.WriteText "      </updg:after>"  
    strmIn.WriteText "  </updg:sync>"  
    strmIn.WriteText "</ROOT>"  
  
    ' Set the command dialect to XML.  
    cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
    strmIn.Position = 0  
    Set cmd.CommandStream = strmIn  
  
    ' Execute the command, open the return stream, and read the result.  
    strmOut.Open  
    strmOut.LineSeparator = adCRLF  
    cmd.Properties("Output Stream").Value = strmOut  
    cmd.Execute , , adExecuteStream  
    strmOut.Position = 0  
    Debug.Print strmOut.ReadText  
    strmOut.Close  
    strmIn.Close  
    conn.Close  
End Sub  
```  
  
## <a name="passing-parameters"></a>매개 변수 전달  
 앞서 살펴보았던 Visual Basic 애플리케이션에서는 매개 변수가 전달되지 않았습니다. 이 응용 프로그램에서 **ContactID** 및 **MiddleName** 값은 매개 변수가 있는 입력으로 updategram에 전달 됩니다.  
  
```vb  
Private Sub Form_Load()  
  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmIn As New ADODB.Stream  
  Dim strmOut As New ADODB.Stream  
  Dim InputContactID As String  
  Dim InputMiddleName As String  
  
  InputContactID = "1"  
  InputMiddleName = "Q."  
  
  ' Open a connection to the instance of SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=(local); database=AdventureWorks; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  
  ' Build the command string in the form of an XML template.  
  SQLxml = "<ROOT xmlns:updg='urn:schemas-microsoft-com:xml-updategram' >"  
  SQLxml = SQLxml & "<updg:header>"  
  SQLxml = SQLxml & "<updg:param name='ContactID'/>"  
  SQLxml = SQLxml & "<updg:param name='MiddleName' />"  
  SQLxml = SQLxml & "</updg:header>"  
  SQLxml = SQLxml & "<updg:sync >"  
  SQLxml = SQLxml & " <updg:before>"  
  SQLxml = SQLxml & "   <Person.Contact ContactID='$ContactID' />"  
  SQLxml = SQLxml & "</updg:before>"  
  SQLxml = SQLxml & "<updg:after>"  
  SQLxml = SQLxml & "<Person.Contact MiddleName='$MiddleName' />"  
  SQLxml = SQLxml & "</updg:after>"  
  SQLxml = SQLxml & "</updg:sync>"  
  SQLxml = SQLxml & "</ROOT>"  
  
  ' Set the command dialect to XML.  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
  ' Open the command stream and write the template to it.  
  strmIn.Open  
  strmIn.WriteText SQLxml  
  strmIn.Position = 0  
  
  Set cmd.CommandStream = strmIn  
  
  ' Execute the command, open the return stream, and read the result.  
  strmOut.Open  
  strmOut.LineSeparator = adCRLF  
  cmd.NamedParameters = True  
  cmd.Parameters.Append cmd.CreateParameter("@ContactID", adBSTR, adParamInput, 1, InputContactID)  
  cmd.Parameters.Append cmd.CreateParameter("@MiddleName", adBSTR, adParamInput, 7, InputMiddleName)  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Debug.Print strmOut.ReadText  
  
End Sub  
```  
  
  
