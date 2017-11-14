---
title: "삭제 메서드 예제 (VBScript) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Delete method [ADO], VBScript example
ms.assetid: 78935d6d-1c1a-4306-a83a-1763210c69f9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f0ef7a792ca53719fdd30164d9742cdede701dd9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="delete-method-example-vbscript"></a>삭제 메서드 (VBScript) 예제
사용 하 여이 예제는 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md) 에서 지정 된 레코드를 제거 하는 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
 다음 예제에는 페이지 ASP (Active Server)를 사용 합니다. 이 완벽 하 게 작동 하는 예제를 보려면 하거나 있어야 AdvWorks.mdb (SDK와 함께 설치 됨) C:\Program Files\Microsoft Platform SDK\Samples\DataAccess\Rds\RDSTest\advworks.mdb에 있는 원본 또는 경로 반영 하도록 예제 코드를 편집 하는 데이터 이 파일의 실제 위치입니다. Microsoft Access 데이터베이스 파일입니다.  
  
 사용 하 여 **찾을** Adovbs.inc 파일을 찾아서을 사용 하려면 디렉터리에 배치 합니다. 잘라내기 메모장 이나 다른 텍스트 편집기에 다음 코드를 붙여 넣고로 저장 **DeleteVBS.asp**합니다. 모든 클라이언트 브라우저에서 결과 볼 수 있습니다.  
  
 예를 실습 하려면 사용 하 여 시도 [AddNew](../../../ado/reference/ado-api/addnew-method-example-vbscript.md) 일부 레코드를 추가 하려면 먼저 예제입니다. 그런 다음 삭제를 시도할 수 있습니다. 모든 클라이언트 브라우저에서 결과 확인 합니다.  
  
```  
<!-- BeginDeleteVBS -->  
<%@ Language=VBScript %>  
<% ' use this meta tag instead of ADOVBS.inc%>  
<!-- METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4"  -->  
<HTML>  
<HEAD>  
<TITLE>ADO Delete Method</TITLE>  
</HEAD>  
<STYLE>  
<!--  
TH {  
   background-color: #008080;   
   font-family: 'Arial Narrow','Arial',sans-serif;   
   font-size: xx-small;  
   color: white;  
   }  
TD {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Arial Narrow','Arial',sans-serif;   
   font-size: xx-small;  
    }  
-->  
</STYLE>  
  
<BODY>   
<H3>ADO Delete Method</H3>  
  
<%  
    ' to integrate this code replace the DataSource value in the connection string  
  
    ' connection and recordset variables  
   Dim Cnxn, strCnxn  
   Dim rsCustomers, strSQLCustomers  
  
    ' create and open connection  
   Set Cnxn = Server.CreateObject("ADODB.Connection")   
   strCnxn="Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
   Cnxn.Open  strCnxn  
    ' create and open recordset  
   Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
   strSQLCustomers = "Customers"  
   rsCustomers.Open strSQLCustomers, Cnxn, adOpenKeyset, adLockOptimistic, adCmdTable  
  
   ' Move to designated record and delete it  
   If Not IsEmpty(Request.Form("WhichRecord")) Then  
      'Get value to move from Form Post method  
      Moves = Request.Form("WhichRecord")  
  
      rsCustomers.Move CInt(Moves)  
      If Not rsCustomers.EOF or rsCustomers.BOF Then  
          ' handle any db errors  
         On Error Resume Next  
         rsCustomers.Delete 1  
         If Cnxn.Errors.Count <> 0 Then  
            Response.Write "Cannot delete since there are related records in other tables."  
            Response.End  
         End If  
         rsCustomers.MoveFirst  
         On Error GoTo 0  
      Else  
         Response.Write "Not a Valid Record Number"  
         rsCustomers.MoveFirst  
      End If  
   End If  
%>  
  
<!-- BEGIN column header row for Customer Table-->  
<TABLE COLSPAN=8 CELLPADDING=5 BORDER=0>  
<TR>  
   <TH>Rec. #</TH>  
   <TH>Company Name</TH>  
   <TH>Contact Name</TH>  
   <TH>City</TH>  
</TR>  
  
   <%   
   ' Display ADO Data from Customer Table   
   ' Loop through Recordset adding one row to HTML Table each pass  
   Dim iCount  
   iCount = 0  
   Do Until rsCustomers.EOF %>  
   <TR>  
     <TD> <%= CStr(iCount) %>  
     <TD> <%= rsCustomers("CompanyName")%> </TD>  
     <TD> <%= rsCustomers("ContactName")%> </TD>  
     <TD> <%= rsCustomers("City")%> </TD>  
   </TR>  
   <%   
     iCount = iCount + 1  
     rsCustomers.MoveNext   
   Loop   
   %>  
</TABLE>  
  
<!-- Do Client side Input Data Validation Move to named record and Delete it -->  
<Center>  
<H4>Clicking Button Will Remove Designated Record</H4>  
<H5>There are <%=rsCustomers.RecordCount%> Records in this Set</H5>  
  
<Form Method=Post Action="Deletevbs.asp" Name=Form>  
   <Input Type=Text Name="WhichRecord" Size=3>   
   <Input Type=Button Name=cmdDelete Value="Delete Record">  
</Form>  
  
</BODY>  
  
<Script Language = "VBScript">  
Sub cmdDelete_OnClick  
   If IsNumeric(Document.Form.WhichRecord.Value) Then  
      Document.Form.WhichRecord.Value = CInt(Document.Form.WhichRecord.Value)  
      Dim Response  
      Response = MsgBox("Are You Sure About Deleting This Record?", vbYesNo,  "ADO-ASP Example")  
  
      If Response = vbYes Then  
         Document.Form.Submit  
      End If  
   Else  
      MsgBox "You Must Enter a Valid Record Number",,"ADO-ASP Example"  
   End If  
End Sub  
</Script>  
  
<%  
    ' clean up  
    If rsCustomers.State = adStateOpen then  
        rsCustomers.Close  
    End If  
    If Cnxn.State = adStateOpen then  
        Cnxn.Close  
    End If  
%>  
</HTML>  
<!-- EndDeleteVBS -->  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

