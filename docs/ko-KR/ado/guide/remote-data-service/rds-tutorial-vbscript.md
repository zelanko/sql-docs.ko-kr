---
title: RDS 자습서 (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 02/14/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: daa7caa4677c33469250e77a1e58e77e697e08c1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="rds-tutorial-vbscript"></a>RDS 자습서 (VBScript)
Microsoft Visual Basic Scripting Edition로 작성 된 RDS 자습서입니다. 이 자습서의 용도 대 한 참조는 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 이 자습서에서는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 및 [.rds입니다 DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 은 디자인 타임에 생성-즉, 다음과 같이 개체 태그에 정의 된: `<OBJECT>...</OBJECT>`합니다. 실행된 모드에서로 만들 수 있습니다는 [CreateObject 메서드 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md) 메서드. 예를 들어는 **.rds입니다 DataControl** 다음과 같은 개체를 만들 수 없습니다.  
  
```  
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
  
## <a name="step-1--specify-a-server-program"></a>1 단계-서버 프로그램 지정  
 VBScript VBScript에 액세스 하 여 실행 중인 IIS 웹 서버 이름을 검색할 수 **Request.ServerVariables** 메서드 Active Server Pages를 사용할 수 있습니다.  
  
```  
"http://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 그러나이 자습서에 대 한 가상 서버를 "해당 서버"를 사용 합니다.  
  
> [!NOTE]
>  데이터 형식에 주의 해야 **ByRef** 인수입니다. VBScript는 지정할 수 없습니다 변수 유형, 항상 통과 해야 하므로 **Variant**합니다. HTTP를 사용 하 여 RDS 하면 Variant를 사용 하 여 호출 하는 경우 비-Variant를 예상 하는 메서드를 전달할 수는 **.rds입니다 DataSpace** 개체 [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) 메서드. 클라이언트 및 서버 양쪽에서 매개 변수 형식을 일치 시켜야 DCOM 또는 프로세스 서버를 사용할 경우 또는 "형식 불일치" 오류가 발생 합니다.  
  
```  
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "http://yourServer")  
```  
  
## <a name="step-2a--invoke-the-server-program-with-rdsdatacontrol"></a>2a 단계-rds.를 사용 하 여 서버 프로그램 호출 DataControl  
 이 예제는 단순히 시연 하는 설명의 기본 동작의 **.rds입니다 DataControl** 지정된 된 쿼리를 수행 하는 것입니다.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b--invoke-the-server-program-with-rdsserverdatafactory"></a>2b 단계-업데이트할을 사용 하 여 서버 프로그램 호출  
  
## <a name="step-3--server-obtains-a-recordset"></a>3 단계-서버가 가져옵니다 레코드 집합을  
  
## <a name="step-4--server-returns-the-recordset"></a>4 단계-서버 레코드 집합 반환  
  
```  
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5--datacontrol-is-made-usable-by-visual-controls"></a>5 단계-DataControl 이루어집니다 사용할 수 있는 시각적 컨트롤에서  
  
```  
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a--changes-are-sent-to-the-server-with-rdsdatacontrol"></a>6a 단계-변경.rds 입니다도 서버에 보내집니다. DataControl  
 이 예제는 단지 설명을 보여 주는 방법을 **.rds입니다 DataControl** 업데이트를 수행 합니다.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
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
  
## <a name="step-6b--changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>6b 단계-변경 내용을 업데이트할으로 서버에 보내집니다.  
  
```  
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **이 자습서의 끝입니다.**  
  
## <a name="see-also"></a>관련 항목:  
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
