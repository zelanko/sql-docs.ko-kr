---
description: '6단계: 서버에 변경 내용이 보내집니다(RDS 자습서).'
title: '6 단계: 서버에 변경 내용 전송 (RDS 자습서) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
author: rothja
ms.author: jroth
ms.openlocfilehash: 33a80f1cf59ff314236e69085c7625521d6f721f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977474"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>6단계: 서버에 변경 내용이 보내집니다(RDS 자습서).
**레코드 집합** 개체를 편집 하는 경우 변경 내용 (즉, 추가, 변경 또는 삭제 된 행)을 서버에 다시 보낼 수 있습니다.  
  
> [!NOTE]
>  ADO 개체 및 Microsoft OLE DB Remoting 공급자를 사용 하 여 RDS의 기본 동작을 암시적으로 호출할 수 있습니다. 쿼리에서는 **레코드 집합**을 반환할 수 있으며 편집 된 **레코드 집합**은 데이터 원본을 업데이트할 수 있습니다. 이 자습서에서는 ADO 개체를 사용 하 여 RDS를 호출 하지는 않지만 다음과 같은 경우를 확인 하는 방법을 보여 줍니다.  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **A 부** 이 경우에는 RDS만 사용 했다고 가정 [합니다. ](../../reference/rds-api/datacontrol-object-rds.md) 이제는 **레코드 집합** 개체가 RDS와 연결 되어 있습니다 **. DataControl**. [SubmitChanges](../../reference/rds-api/submitchanges-method-rds.md) 메서드는 [서버](../../reference/rds-api/server-property-rds.md) 및 [연결](../../reference/rds-api/connect-property-rds.md) 속성이 여전히 설정 된 경우 **레코드 집합** 개체에 대 한 변경 내용으로 데이터 원본을 업데이트 합니다.  
  
```vb
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "https://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **B 파트** 또는 연결 및 **레코드 집합** 개체를 지정 하 여 [RDSServer](../../reference/rds-api/datafactory-object-rdsserver.md) 개체를 사용 하 여 서버를 업데이트할 수 있습니다.  
  
```vb
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **이 자습서의 마지막 부분입니다.**  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft OLE DB Remoting 공급자 (ADO 서비스 공급자)](../appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS 자습서](./rds-tutorial.md)   
 [RDS 자습서(VBScript)](./rds-tutorial-vbscript.md)