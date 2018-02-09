---
title: "추가 및 CreateParameter 메서드 예제 (JScript) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- JScript
helpviewer_keywords:
- CreateParameter method [ADO], JScript example
- Append method [ADO], JScript example
ms.assetid: 37000833-68f4-45f1-b2dd-7f75893d09d9
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f4fb56c40cca35734a4dbc247492f8db3dd86b5
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="append-and-createparameter-methods-example-jscript"></a>추가 및 CreateParameter 메서드 예제 (JScript)
사용 하 여이 예제는 [Append](../../../ado/reference/ado-api/append-method-ado.md) 및 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) 입력된 매개 변수가 있는 저장된 프로시저를 실행 하는 메서드. 메모장 이나 다른 텍스트 편집기에 다음 코드를 잘라내어 하십시오로 저장 **붙여 넣고 AppendJS.asp**합니다.  
  
```  
<!-- BeginAppendJS -->  
<%@LANGUAGE="JScript" %>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
<head>  
    <title>Append and CreateParameter Methods Example (JScript)</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
-->  
</style>  
</head>  
  
<body>  
<h1>Append and CreateParameter Methods Example (JScript)</h1>  
<%  
    // verify user-input   
    var iRoyalty = parseInt(Request.Form("RoyaltyValue"));  
    if (iRoyalty > -1)  
    {  
  
        // connection, recordset and command variables  
        var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='pubs';Integrated Security='SSPI';";  
        var Cnxn = Server.CreateObject("ADODB.Connection");  
        var cmdByRoyalty = Server.CreateObject("ADODB.Command");  
        var rsByRoyalty = Server.CreateObject("ADODB.Recordset");  
        var rsAuthor = Server.CreateObject("ADODB.Recordset");  
        // display variables  
        var strMessage;  
  
        try  
        {  
            // open connection and set cursor location  
            Cnxn.Open(strCnxn);  
            Cnxn.CursorLocation = adUseClient;  
  
            // command object initial parameters  
            cmdByRoyalty.CommandText = "byroyalty";  
            cmdByRoyalty.CommandType = adCmdStoredProc;  
  
            // create the new parameter and append to  
            // the Command object's parameters collection  
            var prmByRoyalty = cmdByRoyalty.CreateParameter("percentage", adInteger, adParamInput);  
            cmdByRoyalty.Parameters.Append(prmByRoyalty);  
            prmByRoyalty.Value = iRoyalty;  
  
            cmdByRoyalty.ActiveConnection = Cnxn;  
  
            // execute command  
            rsByRoyalty = cmdByRoyalty.Execute();  
  
            // display results  
            rsAuthor.Open("Authors", Cnxn);  
  
            while (!rsByRoyalty.EOF)  
            {  
                rsAuthor.Filter = "au_id='" + rsByRoyalty.Fields("au_id") + "'";  
  
                // start new line  
                strMessage = "<P>";  
  
                // recordset data  
                strMessage += rsAuthor.Fields("au_fname") + " ";   
                strMessage += rsAuthor.Fields("au_lname") + " ";  
  
                // end the line  
                strMessage += "</P>";  
  
                // show result  
                Response.Write(strMessage);  
  
                // et next record  
                rsByRoyalty.MoveNext;  
            }  
        }  
        catch (e)  
        {  
            Response.Write(e.message);  
        }  
        finally  
        {  
            // clean up  
            if (rsByRoyalty.State == adStateOpen)  
                rsByRoyalty.Close;  
            if (rsAuthor.State == adStateOpen)  
                rsAuthor.Close;  
            if (Cnxn.State == adStateOpen)  
                Cnxn.Close;  
            rsByRoyalty = null;  
            rsAuthor = null;  
            Cnxn = null;  
        }  
    }  
%>  
  
<hr>  
  
<form method="POST" action="AppendJS.asp" id=form1 name=form1>  
  <p align="left">Enter royalty percentage to find (e.g., 40): <input type="text" name="RoyaltyValue" size="5"></p>  
  <p align="left"><input type="submit" value="Submit" name="B1"><input type="reset" value="Reset" name="B2"></p>  
</form>  
  
</body>  
  
</html>  
<!-- EndAppendJS -->  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Append 메서드 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [CreateParameter 메서드 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)
