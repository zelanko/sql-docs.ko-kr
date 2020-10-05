---
description: RDS 자습서(VBScript)
title: RDS 자습서 (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ad7fcb2bb63d77bd50c89f11e9b818439b0d1d0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721404"
---
# <a name="rds-tutorial-vbscript"></a>RDS 자습서(VBScript)
Microsoft Visual Basic Scripting Edition으로 작성 된 RDS 자습서입니다. 이 자습서의 용도에 대 한 설명은 [RDS 자습서](./rds-tutorial.md)를 참조 하십시오.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
 이 자습서에서는 [RDS입니다. DataControl](../../reference/rds-api/datacontrol-object-rds.md) 및 [RDS. 스페이스](../../reference/rds-api/dataspace-object-rds.md) 는 디자인 타임에 생성 됩니다. 즉,와 같이 개체 태그로 정의 됩니다 `<OBJECT>...</OBJECT>` . 또는 런타임에 [RDS (CreateObject 메서드)](../../reference/rds-api/createobject-method-rds.md) 메서드를 사용 하 여 만들 수 있습니다. 예: **RDS. ** 다음과 같이 DataControl 개체를 만들 수 있습니다.  
  
```vb
Set DC = Server.CreateObject("RDS.DataControl")  
   <!-- RDS.DataControl -->  
   <OBJECT   
      ID="DC1" CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E33">  
   </OBJECT>  
  
   <!-- RDS.DataSpace -->  
   <OBJECT   
      ID="DS1" WIDTH=1 HEIGHT=1  
      CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
   </OBJECT>  
  
   <SCRIPT LANGUAGE="VBScript">  
  
   Sub RDSTutorial()  
   Dim DF1   
```  
  
## <a name="step-1---specify-a-server-program"></a>1 단계-서버 프로그램 지정  
 Vbscript는 VBScript 요청에 액세스 하 여 실행 중인 IIS 웹 서버의 이름을 검색할 수 있습니다 **. ServerVariables** 메서드는 Active Server 페이지에서 사용할 수 있습니다.  
  
```vb
"https://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 그러나이 자습서에서는 허수 서버 "해당 서버"를 사용 합니다.  
  
> [!NOTE]
>  **ByRef** 인수의 데이터 형식에 주의 합니다. VBScript에서는 변수 형식을 지정할 수 없으므로 항상 **Variant**를 전달 해야 합니다. HTTP를 사용 하는 경우 rds를 사용 하 여 호출 하는 경우 비 변형이 필요한 메서드에 Variant를 전달할 수 있습니다 **. 공간** 개체 [CreateObject](../../reference/rds-api/createobject-method-rds.md) 메서드입니다. DCOM 또는 in-process 서버를 사용 하는 경우 클라이언트 및 서버 쪽의 매개 변수 형식과 일치 해야 합니다. 그렇지 않으면 "형식 불일치" 오류가 표시 됩니다.  
  
```vb
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "https://yourServer")  
```  
  
## <a name="step-2a---invoke-the-server-program-with-rdsdatacontrol"></a>2a 단계-RDS를 사용 하 여 서버 프로그램을 호출 합니다. DataControl  
 이 예제는 단순히 RDS의 기본 동작을 보여 주는 주석입니다 **. DataControl** 은 지정 된 쿼리를 수행 하는 것입니다.  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b---invoke-the-server-program-with-rdsserverdatafactory"></a>2b 단계-RDSServer. DataFactory를 사용 하 여 서버 프로그램을 호출 합니다.  
  
## <a name="step-3---server-obtains-a-recordset"></a>3 단계-서버에서 레코드 집합을 가져옵니다.  
  
## <a name="step-4---server-returns-the-recordset"></a>4 단계-서버에서 레코드 집합 반환  
  
```vb
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5---datacontrol-is-made-usable-by-visual-controls"></a>5 단계-visual 컨트롤에서 사용할 수 있는 DataControl  
  
```vb
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a---changes-are-sent-to-the-server-with-rdsdatacontrol"></a>6a 단계-변경 내용이 RDS를 사용 하 여 서버로 전송 됩니다. DataControl  
 이 예제는 단순히 RDS를 보여 주는 주석입니다 **. DataControl** 은 업데이트를 수행 합니다.  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial6A()  
Dim RS  
DC1.Refresh  
...  
Set RS = DC1.Recordset  
' Edit the Recordset object...  
' The SERVER and CONNECT properties are already set from Step 2A.  
Set DC1.SourceRecordset = RS  
...  
DC1.SubmitChanges  
```  
  
## <a name="step-6b---changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>6b 단계-RDSServer를 사용 하 여 서버에 변경 내용을 보냅니다. DataFactory  
  
```vb
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **이 자습서의 마지막 부분입니다.**  
  
## <a name="see-also"></a>참고 항목  
 [RDS 자습서](./rds-tutorial.md)